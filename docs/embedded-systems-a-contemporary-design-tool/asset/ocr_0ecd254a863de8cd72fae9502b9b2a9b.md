When current is leaving the device (driver or receiver), it is said to be sourcing current; when current enters the device (driver or receiver), it is said to be sinking current. We define current leaving the device as negative and current entering the device as positive. This is an arbitrary, but consistent, labeling. We can see these in Figure 2.6.

![](bbox=[0.25, 0.16, 0.5, 0.25])

# Figure 2.6 Sourcing and Sinking Current

In the first case, inverter Inv1 is sourcing current to Inv2, which is sinking that current. With respect to Inv1, the current, I, will be negative; and with respect to Inv2 it will be positive. In the second case, the roles are reversed; Inv1 is sinking current (which will be viewed positive) that is being sourced by Inv2 (which will be viewed as negative). Once again, we use the bubbles on the gate to indicate the logical 0 state.

The data sheet for the device will give the specifications in Table 2.2.

| | Current | Voltage |
|---|---|---|
| IOL | 8 mA (entering) | @ Vol = 0.5 VDC |
| IOH | -400 µA (leaving) | @ Voh = 3.4 VDC |
| IIL | -400 µA (leaving) | @ Vil = 0.4 VDC |
| IIH | -20 µA (entering) | @ Vih = 2.7 VDC |

Starting from the data sheet, one can compute the fan-out for the SN74LS04 device. Two cases must be considered when computing the fan-out for the device, when the output is in the logical 0 state and when it is in the logical 1 state. When specifying the fan-out for the device, we always use the lower of the two values.

# Logic 0 State

When the output is at a logical 0 level, the data sheet specifies that the device can sink 8 mA, and when an input is at a logical 0 level, it sources –400 µA. Thus, when its output is in the logical 0 state, SN74LS04 can sink the current from 20 similar devices.

```
fan-out = | 8 mA / -400 µA |
= 20
```

# Logic 1 State

When the output is in the logic 1 state, the data sheet specifies that the device can source –400 µA, and when an input is at logic 1 it sinks 20 µA.