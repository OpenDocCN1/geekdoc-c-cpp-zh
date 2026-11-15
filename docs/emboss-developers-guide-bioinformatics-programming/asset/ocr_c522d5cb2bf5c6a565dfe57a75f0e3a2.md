```
FP /X65923/
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
//
```

The command line session is below:

```
% qatest.pl -simple -testfile=secret_2.dat secret-ex2
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

# Test 3

Write the result in GCG format by using the qualifier -osformat:

```
ID secret-ex3
UC Write the result in GCG format by using the qualifier '-osformat'.
AP secret
CL -osf gcg
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.gcg
FP /X65923/
//
```

The command line session is below:

```
% qatest.pl -simple -testfile=secret_3.dat secret-ex3
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

# Test 4

Write the result in GCG format by specifying the format in the output USA on the command line:

```
ID secret-ex4
UC Write the result in GCG format by specifying the format
UC in the output USA on the command line.
AP secret
CL -outseq gcg::x65923.gcg
IN embl:x65923
FI stderr
FC = 2
```