![](bbox=[0.28, 0.07, 0.68, 0.24])

# Figure 2.8 Driving to the Logical 1 State

# Logical 0

If the output of the Driver is in the logical 0 state, the currents will now appear as in Figure 2.9. Observe that bubbles on the logic symbols are altered to reflect the logical 0 values on the respective gates. Once again, summing currents at node N1 gives,

```
-i1 + i2 + i3 = 0
(2.4)
```

For this case, i2 is not 0 and must be taken into account.

```
i3 = i1 - i2
i3 = 15 mA - 10 mA
fan-out = i3 / i4
= 5 mA / 20 µA
= 250
```

![](bbox=[0.28, 0.59, 0.68, 0.75])

# Figure 2.9 Driving to the Logical 0 State

In the logical 0 case, the driver must be able to sink the current from the LED as well as that from the collection of inverters. After the LED current has been taken into account, substantially less remains available for the inverters. As this analysis illustrates, in the logical 0 case, the fan-out is reduced to 250. Thus, we must use the smaller of the two figures in any design. The fan-out for the circuit is determined to be 250.