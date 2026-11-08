The show ip sla statistics 1 command provides some basic history through a counter of successes and failures, as shown in Example 26-14. In addition to the return code and RTT of the most recent operation, you get a counter of successes and failures of past operations. So, you can get a sense of whether the pings have been failing or not.

# **Example 26-14** *Historical Success/Failure Counters with IP SLA*

```
R1# show ip sla statistics 1

IPSLAs Latest Operation Statistics


IPSLA operation id: 1
        Latest RTT: 16 milliseconds
Latest operation start time: 12:40:39 EST Tue Jan 5 2016
Latest operation return code: OK
Number of successes: 7
Number of failures: 0
Operation time to live: Forever
```