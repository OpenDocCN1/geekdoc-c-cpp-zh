![](bbox=[0.26, 0.07, 0.69, 0.23])

Figure 10.22 Basic Combinational Logic Circuit With Path to Multiple Outputs Sensitized

C can be tested in a similar manner and the remaining paths to the two outputs are tested as before. By holding B to a logical 1 and C to a logical 0, we sensitize the path for A. The same set of inputs also sensitizes the path for D.

To debug or troubleshoot, assume a stuck-at fault on the output of either E or F. To begin, A and D are placed in the logical 0 state and C in the logical 1 state. The net expressing the conjunction of A and B should be in the logical 0 state.

Exercising input B through a 1-0-1 sequence should cause corresponding changes in both outputs. A change in only one provides two pieces of information: the net expressing the conjunction of B and C is functioning properly, and most likely the fault is with the output of the unchanged OR gate.

The diagnosis is confirmed by placing signal C in the logical 0 state and the signal B in the logical 1 state, thereby disabling the lower AND gate (and the corresponding output nets) and sensitizing the path from A. Either A or D can then be toggled as appropriate.

# 10.16 BRIDGE FAULTS

Recall that a bridge fault occurs when a connection among two or more signals exists where none had been originally intended. Generally, such faults will be identified during a good manufacturing defects test that would detect the unintended low-impedance path. During debugging, without the aid of such a test, one must fall back on one or more variants of a functional test.

A card edge input bridge, fault such as the one in Figure 10.23, can be tested using a path sensitization scheme coupled with a test using complementary values for signals B and C. We debug or troubleshoot the fault in a similar way, testing whether first one and then the other (B or C) can propagate the intended value to the circuit output.

![](bbox=[0.26, 0.78, 0.65, 0.88])

Figure 10.23 Bridge Fault