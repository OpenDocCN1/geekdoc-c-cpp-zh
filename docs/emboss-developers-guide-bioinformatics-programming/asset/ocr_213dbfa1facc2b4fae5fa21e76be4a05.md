```
Tests total: 0.
```

If it succeeds, all files are deleted unless the test entry included a DL keep line, or -keep was specified on the command line.

If it fails, it will report why and all results will be saved in the results directory for inspection. You would check, for example, myprogram-ex, then identify the problem, update the test definition and try again until it works.

A typical session looks something like this:

```
../scripts/qatest.pl -without=srs
Tests total: 1586 pass: 1586 fail: 0
Skipped: 12 check: 1 embassy: 0 requirements: 11
Missing documentation html: 0 text: 0 sourceforge: 0
Time: 677 seconds
```

# ## 7.2.4 Useful files and directories

There are some useful files held under /emboss/test/. The directories are as follows:

+   - **acd**: ACD files for test applications. These are used for testing ACD file parsing. You will not need this directory unless you extend ACD.
+   - **data**: The directory for test data that has already been mentioned. Your test data input files should go in here, or in a sub-directory beneath it.
+   - **gb**: Some GenBank data files in NBRF/GCG database format.
+   - **qa**: The directory from which all tests must be run. Application output files are written to their own results directory underneath this, and are deleted on successful test completion unless otherwise stated.
+   - **rc**: This directory is used for database and resource definition tests. You will not need it.
+   - **swnew**: Files from the SwissProt database used to make the tsw test database.
+   - **embl**: Files from the EMBL database used to make the tembl test database.
+   - **genbank**: Some GenBank data files used to make the tgenbank test database.
+   - **memtest**: Files for tracing memory leaks: you will not need this.
+   - **pir**: Data files from the PIR database used to make the tpir test database.
+   - **swiss**: Data files from the SwissProt database.
+   - **wormpep**: Data files from the WormPep (worm peptide) database.