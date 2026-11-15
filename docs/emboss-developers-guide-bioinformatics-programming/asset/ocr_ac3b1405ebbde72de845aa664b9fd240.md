# 9.5 Quality assurance tests

Quality assurance tests for seqret are defined in the file:

```
.../emboss/emboss/test/qatest.dat
```

The test data for the application is given under the /test directory and consists of input files, application parameters and the corresponding output files.

You'll see from inspecting the file that many tests are defined for the application, testing it under all sorts of input conditions in order to be as robust as possible. These are performed frequently to ensure the applications work as advertised and are not broken by (e.g.) recent changes to the library code.

Quality assurance testing, including how to write entries in qatest.dat, is covered in detail elsewhere (Chapter 7, Quality assurance).

# Test 1

This test extracts an entry from a database and writes it to a file:

```
ID seqret-ex1
UC Extract an entry from a database and write it to a file:
AP seqret
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.fasta
FP /X65923/
//
```

The command line session is below:

```
% qatest.pl -simple -testfile=seqret_1.dat seqret-ex1
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

# Test 2

Display the contents of the sequence on the screen:

```
ID seqret-ex2
UC Display the contents of the sequence on the screen:
AP seqret
IN embl:x65923
IN stdout
FI stdout
```