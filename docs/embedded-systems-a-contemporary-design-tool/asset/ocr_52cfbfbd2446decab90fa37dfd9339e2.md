# 10.18 SCAN DESIGN TESTING

The strategy for debugging sequential machines using scan design techniques is rather straightforward. The flip-flops are at the heart of the circuit and the technique, so it is best to ensure that they are functioning properly first. We repeat the drawing of a state machine with scan design support in Figure 10.28.

![](bbox=[0.28, 0.2, 0.8, 0.68])

Figure 10.28 Basic State Machine with Scan Path Logic

select, test scan in scan out

Initially the select input is placed into the test mode. With the flip-flops configured as a shift register, a pattern of alternating 0's and 1's is entered on the scan in input and monitored on the scan out output. If the pattern that has been entered appears properly on the output, we assume that the devices are working correctly and can proceed.

If the output appears as a constant 0 or 1, then we infer that one of the devices (or its input) is malfunctioning. If manual access to the individual flip-flop pins is possible, we debug by probing those signals. If such access is not available, little can be done.

Assuming that the necessary access is available, the first debugging step is to verify the reset signal (if it is present) to ensure that the machine is not being held in the reset state.