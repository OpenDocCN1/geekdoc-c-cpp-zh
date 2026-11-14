![](bbox=[0.26, 0.08, 0.54, 0.31])

In real-time embedded applications, one of the major design concerns is meeting time specifications. Although in some cases the concern is about a signal arriving too quickly, generally the focus is on trying to ensure that the signal arrives before a specified deadline. Thus, when modeling a combinational circuit, we use the longer of the two delays, specifying that value as simply, τpd.

The syntax for modeling such a delay in Verilog is given by

```
Syntax
# delay LHS = RHS; // RHS changes and is assigned to LHS after
// delay
```

The following code fragment illustrates the inclusion of a delay of two time units in a part model.

```
parameter propagationDelay = 2;
not #propagationDelay myNot (sigOut, sigIn);
```

Verilog also supports the inclusion of device rise time, fall time, and delay. The syntax is given as

```
Syntax
# (rise time, fall time, delay) device;
```

The code fragment in Figure 2.13 illustrates the inclusion of a rise time of one time unit, a fall time of two time units, and a delay of three time units in a part model.

```
parameter riseTime = 1;
parameter fallTime = 2;
parameter propagationDelay = 3;
not #(riseTime, fallTime, propagationDelay)
myNot (sigOut, sigIn);
```

Figure 2.13 Modeling Rise Time, Fall Time, and Propagation Delay