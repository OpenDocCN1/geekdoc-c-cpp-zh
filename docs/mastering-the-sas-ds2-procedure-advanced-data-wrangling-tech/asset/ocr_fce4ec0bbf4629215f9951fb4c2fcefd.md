# 7.3 Analyzing Performance with the SAS Log

# 7.3.1 Obtaining Performance Statistics

The default option settings in SAS provide a modulus of performance reporting in the SAS log. Here is an example of the default performance statistics reported under Linux (the operating system used by SAS University Edition):

Here is an example of standard performance statistics in the SAS log:

```
NOTE: PROCEDURE DS2 used (Total process time):
real time 2.35 seconds
cpu time 0.17 seconds;
```

You will notice that SAS produces performance statistics only after the QUIT statement for PROC DS2 session, so if you have included several DS2 steps within the boundaries, you only get aggregate results for the entire process. For troubleshooting and tuning, try placing each DS2 program in its own PROC DS2 session to obtain more granular results.

When your performing is poorly, the problem usually boils down to one or more of the factors:

+   * CPU
* memory
* I/O
* network latency

When tracking performance issues, or trying to tune your code, setting OPTIONS FULLSTEM can provide more detailed information that can help you narrow down the areas where the system might be having problems. You can then try writing code in different ways with the intent of mitigating performance problems by alleviating any problems detected.

Here is an example of the performance statistics reported using FULLER:

```
NOTE: PROCEDURE DS2 used (Total process time):
real time 2.35 seconds
user cpu time 0.10 seconds
system cpu time 0.07 seconds
memory 5738.84k
OS Memory 30268.00k
Timestamp 02/14/2016 10:23:11 AM
Step Count 87 Switch Count 50
Page Faults 0
Page Reclaims 1925
Page Swaps 0
Voluntary Context Switches 2648
Involuntary Context Switches 191
Block Input Operations 0
Block Output Operations 0
```