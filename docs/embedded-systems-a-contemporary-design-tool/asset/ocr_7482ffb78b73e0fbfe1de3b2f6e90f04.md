+   path sensitizing

One simple and effective approach for determining the necessary stimuli for both test and troubleshooting is based on what is called path sensitizing. With such an approach, first identify a path from the signal under test (or fault) to an observable circuit output. Next choose values for the remaining signals, as appropriate, such that any changes in the circuit output under test are only a function of the signal being tested.

We will begin with the two basic logic gates in Figure 10.10 as a first model. Although we are using logic gates to illustrate the method, they can easily model more general conjunctive or disjunctive relationships between inputs and output in either hardware or software.

![](bbox=[0.285, 0.235, 0.455, 0.345])

Figure 10.10 Path Sensitizing

For an AND (conjunctive) function, one must ensure that all inputs, except the one under test, are in the logical 1 state. Assume that we wish to test the behavior of input signal A. We place the input signal B into the logical 1 state. Under such a condition, any changes to the output, C, are only a function of changes in the input, A. Thus, a stuck-at condition on A is directly observable on C. That is, if the signal A is changed and the corresponding change is not reflected on C, one can conclude that a stuck-at condition exists on A. We state that the fault has been forwarded to an observable output.

+   fault has been forwarded

For an OR (disjunctive) function, we sensitize the path by placing all nets not on the path in the logical 0 state. Once again, changes in the output reflect only those on input A, and a stuck-at condition on A appears on C.

# 10.13.1 Single Variable-Single Path

Path sensitizing can be used to test and debug the accompanying circuit in Figure 10.11.

![](bbox=[0.285, 0.615, 0.555, 0.685])

Figure 10.11 Basic Combinational Logic Circuit

# 10.13.1.1 Testing

To test the circuit, one must show that signals A, B, and C will propagate to D or are blocked subject to the logical constraints of the circuit. Input C is a logical choice to start with since it is the simplest. If debugging is necessary, hypothesize a stuck-at state on the output D and work backwards.

Going forward for the moment to test C, one must ensure that the upper leg of the AND gate is in the logical 1 state, thereby sensitizing the lower path to the signal C. The required system state can be achieved by assigning either A or B a value of logical 1. The state of the other input does not matter.

That condition is represented with the don't care value on B in Figure 10.12.