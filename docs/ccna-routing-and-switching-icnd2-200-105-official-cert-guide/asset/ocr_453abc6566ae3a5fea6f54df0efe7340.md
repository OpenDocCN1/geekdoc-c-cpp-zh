```
```
history lives-kept 1                         !
!
ip sla schedule 1 life forever start-time now
```
```

Also notice the ip sla schedule command at the end of Example 26-12 as well. IP SLA uses a concept of configuring the IP SLA operation with a number, with many subcommands defining the probe, as seen in the majority of the example. Separately, as shown at the bottom of the example, the ip sla schedule global configuration command tells IOS when to run the operation: when to start, and when to stop. An operation can be started at a certain date and time, or in so much time from when the command is issued, or to just start now (as is shown in the example with the start-time now parameters). This command can also limit how long the probe runs; in this case, the probe runs forever, which means until the engineer issues a command like no ip sla schedule 1 to remove the command from the configuration.

# ## Troubleshooting Using IP SLA Counters

The IP SLA ICMP-Echo operation does the equivalent of a single ping to another address, on a timed basis. So how does that help you troubleshoot problems, particularly in comparison to just using the ping command from the CLI? This section shows how, by taking a closer look at the data made available by IP SLA.

To begin, take a look at the most basic IP SLA show command, the show ip sla summary command, as listed in Example 26-13. The command lists a single line of output per SLA operation. It lists some configuration information, namely the address to which the ICMP Echo is being sent. It also lists the two key pieces of information you have seen many times in the output of ping commands: an indication of whether the Echo Request received a response, and the Round Trip Time (RTT), which measures the delay from sending the ICMP Echo Request until receiving the matching ICMP Echo Reply. With this command, the success or failure is shown in the Return Code column, with OK meaning that an Echo Reply was received.

# **Example 26-13 Displaying the Return Code State and RTT with Basic IP SLA Commands**

```
```
R1# show ip sla summary
IPSLAs Latest Operation Summary
Codes: * active, ^ inactive, ~ pending
ID           Type        Destination       Stats       Return      Last
                                           (ms)        Code        Run
-----------------------------------------------------------------------
*1           icmp-echo   10.1.3.2          RTT=124     OK          15 seconds ago
*2           icmp-echo   10.1.3.2          RTT=184     OK          11 seconds ago
R1# ping 10.1.3.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.3.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/4 ms
R1#
```
```