# logmerge
Automatically exported from https://code.google.com/p/logmerge
The alternative download page is on [FossHub Code](http://code.fosshub.com/logmerge/downloads).

# logmerge
Automatically exported from code.google.com/p/logmerge

Small and powerful script to merge two or more logfiles so that multilined entries appear in the correct chronological order without breaks of entries. Optional arguments control an adding of descriptive fields at the beginning of each line in the resulting combined logfile. Reading of `.gz`/`.bz2` files is available.

## Examples

### 1. Merge all Apache error files

<pre>
./logmerge --apache-error ./error.log* > all.log
</pre>

Merge all `error.log*` Apache files, including `gzip`ed files too, and store to the resulting file. The `--apache-error` option considers that each line seems like the example below, makes the marker containing the sortable timestamp `20100423221421` corresponding to the original one:

<pre>
[Fri Apr 23 22:14:21 2010] <the rest of the entry>
</pre>

### 2. Merge all Apache access files===

<pre>
find /export/home/ -name 'access.log' | xargs ./logmerge -f -n --apache-access > all.log
</pre>

Find all last `access.log` Apache files from all home directories within the `/export/home` directory, merge them chronologically and store to the resulting file. Additionally each line of the file will begin with a filename and line number within the original file. 
The utility considers that the Apache's access logfiles consist of the following logentries and transforms the found timestamp to the sortable form `20080215141549`: 

<pre>
<the begin of the entry> [15/Feb/2008:14:18:49 +0300] <the rest of the entry>
</pre>

### 3. Merge multiline entries from several files chronologically===

<pre>
./logmerge -f -n log/*.log | gzip -c > all.gz
</pre>

Merge all files located within the `log/` directory and pass the result to archive. The filename and the line number will be added at the beginning of each line in the resulting file. By default the utility assumes that each logentry begins with a timestamp and can occupy more than a single line (e.g.: Java's stack traces like below): 

<pre>
05/21/2012 21:54:41.070 <the rest of the entry>
java.lang.Throwable
        at boo.hoo.StackTrace.bar(StackTrace.java:223)
        at boo.hoo.StackTrace.foo(StackTrace.java:218)
        at boo.hoo.StackTrace.main(StackTrace.java:54)
...
</pre>

<http://mac.softpedia.com/get/Developer-Tools/logmerge.shtml>
