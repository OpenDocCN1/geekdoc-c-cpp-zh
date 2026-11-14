Note that only 10 address bits are needed for the column address since the memory has 1 K columns. The timing of the normal row and column address enable signals is given in Figure 4.26.

![](bbox=[0.21, 0.16, 0.9, 0.49])

The signal timing is set such that the addresses are generated on phase 1 of the clock. The row and column address enable signals are asserted on the same phase. RAS and CAS are generated on phase 2 of the clock. The two enable signals can be generated using the state machine in Figure 4.27.

![](bbox=[0.18, 0.64, 0.9, 0.77])

# 4.12.3 Refresh Arbitration

The refresh address is independent from that used by the normal read or write operations. Consequently, there is a nonzero probability that either a refresh or normal read or write operation may be in progress when the other is requested or that there may be a collision in