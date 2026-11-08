```
Routing for Networks:
  10.0.0.0
  Routing Information Sources:
    Gateway           Distance          Last Update
    10.1.4.3               90            00:22:32
    10.1.5.2               90            00:22:32
  Distance: internal 90 external 170
```

To see the shorthand repeat of the EIGRP configuration, look toward the end of the exam-ple, under the heading Routing for Networks. In this case, the next line that lists 10.0.0.0 is a direct reference to the **network 10.0.0.0** configuration command shown in Example 10-1.

For configurations that use the wildcard mask option, the format of the **show ip protocols** command differs a little. Example 10-5 shows an excerpt of the **show ip protocols** com-mand from R3. R3 uses the three **network** commands shown earlier in Example 10-2.

![](bbox=[0.07, 0.37, 0.14, 0.43])

# **Example 10-5** EIGRP Wildcard Masks Listed with **show ip protocols** on R3

```
R3# show ip protocols
! Lines omitted for brevity

  Automatic Summarization: disabled
  Maximum path: 4
  Routing for Networks:
    10.1.3.0/24
    10.1.4.0/24
    10.1.6.0/24
! Lines omitted for brevity
```

To interpret the meaning of the highlighted portions of this **show ip protocols** command, you have to do a little math. The output lists a number in the format of **/x** (in this case, **/24**). It represents a wildcard mask with x binary 0s, or in this case, 0.0.0.255.

Before moving on from the **show ip protocols** command, take a moment to read some of the other details of this command's output from Example 10-4. For instance, it lists the EIGRP router ID (RID), which for R1 is 10.1.5.1. EIGRP allocates its RID just like OSPF, based on the following:

![](bbox=[0.07, 0.73, 0.14, 0.78])

+   1. The value configured with the **eigrp router-id** *number* EIGRP subcommand
+   2. The numerically highest IP address of an up/up loopback interface at the time the EIGRP process comes up
+   3. The numerically highest IP address of a nonloopback interface at the time the EIGRP process comes up

The only difference compared to OSPF is that the EIGRP RID is configured with the **eigrp router-id** *value* router subcommand, whereas OSPF uses the **router-id** *value* subcom-mand.