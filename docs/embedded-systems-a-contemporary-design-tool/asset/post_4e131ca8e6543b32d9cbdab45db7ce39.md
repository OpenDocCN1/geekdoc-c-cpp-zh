
The set of input and corresponding output signals combined with the order in which they are applied form the basis for the test cases in the test procedure. While mainly informal during early testing and debugging, the set is called and formalized during the later phases of the design cycle.

As the process now unfolds, we will look first at testing and debugging of combinational logic and then at sequential logic. But first we will have a short digression.

### 10.11.4 Sudden Failure during Debugging

Let's now assume that we have been working on the circuit for some time and have been approaching debugging and integration tasks methodically, adding and debugging one functional subcomponent at a time. So far, three of the five modules in the system have been debugged and integrated, and now the fourth is added. The new module does not work (although it worked as a stand-alone component). Furthermore, the first three modules now fail to work properly. If module 4 is disconnected from the circuit, the original components once again work properly. Repeated tests on module 4 alone fail to identify any possible faults. What could the problem be?

Consider a simple model. A Thévenin equivalent circuit can be developed for each of the five components in the system. As each one is integrated, the system can be modeled as in the sequence of drawings shown in Figure 10.8.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_583_0.png)

Figure 10.8 Modeling a System as Components are Added

For the current discussion, assume that the Thévenin equivalent impedance of each module is the same. Initially, the current demand is given as:

```
$$I_1 = \frac{V_{CC}}{Z}$$
```

The second module is now added. Since the impedances are in parallel, the current requirement is now:

```
$$I_2 = 2 \cdot \frac{V_{CC}}{Z} = 2 \cdot I_1$$
```

As modules are continuously added, the equivalent impedance continues to decrease. After the fourth module is added, the current required is now:

```
$$I_4 = 4 \cdot \frac{V_{CC}}{Z} = 4 \cdot I_1$$
```

The Thévenin model for the power supply is given in Figure 10.9.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_584_0.png)

Figure 10.9 Power Supply Basic Model

It is now evident that as the current demand increases, there will be an increasingly larger drop across the internal impedance of the power supply, with a consequent decrease in the output voltage. To remedy the problem, one must increase the current limit if a bench supply is being used or modify the design of the supply if that is required to provide a greater drive capability.

In the next several sections, we will apply some of the concepts that we learned earlier in our discussions of testing combinational and sequential logic to the problem of debugging new designs. We will find that the problems of test and debug are very similar and that we can utilize much of the same strategy.

## 10.12 TESTING AND DEBUGGING COMBINATIONAL LOGIC

One objective of the early test cases is to show that the circuit and software modules, or subsystem and system, meet the core behavioral requirements. Boundary condition testing occurs later in the process. The test stimuli should reflect the basic requirements and should, in theory, yield the anticipated output signals. One should not exhaustively apply all input patterns. Rather, another early goal is to ensure that all possible paths from input to output are verified.

When a test fails, the debugging process starts. At this stage, it is not known if the design for the module being tested is correct. Sherlock Holmes, the fictional detective, proposed an interesting strategy that can easily be applied to debugging and troubleshooting: eliminate everything that is not causing the fault and what's left is the culprit. Thus, when debugging, one should use test stimuli that can eliminate circuit paths that are not contributing to a fault being isolated. Such knowledge derives from the clear understanding of the behavior of the module being tested — white box testing.

> eliminate everything that is not causing the fault and what's left is the culprit

In contrast, in formal test, one begins with the assumption that the circuit is good, and the objective is to prove such is the case by confirming that each path can pass the necessary signals properly. The test vectors used in test are often a subset of those used during debugging.

## 10.13 PATH SENSITIZING

To be able to effectively test or debug a circuit, one must apply the appropriate test signals (test vector) and observe the consequences of such signals on the circuit. A signal is said to be *directly observable* if its behavior can be seen (tested) directly at card edge or test point and *indirectly observable* if it can only be seen through some intermediate component.

> directly observable indirectly observable

- path sensitizing

One simple and effective approach for determining the necessary stimuli for both test and troubleshooting is based on what is called path sensitizing. With such an approach, first identify a path from the signal under test (or fault) to an observable circuit output. Next choose values for the remaining signals, as appropriate, such that any changes in the circuit output under test are only a function of the signal being tested.

We will begin with the two basic logic gates in Figure 10.10 as a first model. Although we are using logic gates to illustrate the method, they can easily model more general conjunctive or disjunctive relationships between inputs and output in either hardware or software.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_585_0.png)

Figure 10.10 Path Sensitizing

For an AND (conjunctive) function, one must ensure that all inputs, except the one under test, are in the logical 1 state. Assume that we wish to test the behavior of input signal A. We place the input signal B into the logical 1 state. Under such a condition, any changes to the output, C, are only a function of changes in the input, A. Thus, a stuck-at condition on A is directly observable on C. That is, if the signal A is changed and the corresponding change is not reflected on C, one can conclude that a stuck-at condition exists on A. We state that the fault has been forwarded to an observable output.

- fault has been forwarded

For an OR (disjunctive) function, we sensitize the path by placing all nets not on the path in the logical 0 state. Once again, changes in the output reflect only those on input A, and a stuck-at condition on A appears on C.

### 10.13.1 Single Variable-Single Path

Path sensitizing can be used to test and debug the accompanying circuit in Figure 10.11.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_585_1.png)

Figure 10.11 Basic Combinational Logic Circuit

### 10.13.1.1 Testing

To test the circuit, one must show that signals A, B, and C will propagate to D or are blocked subject to the logical constraints of the circuit. Input C is a logical choice to start with since it is the simplest. If debugging is necessary, hypothesize a stuck-at state on the output D and work backwards.

Going forward for the moment to test C, one must ensure that the upper leg of the AND gate is in the logical 1 state, thereby sensitizing the lower path to the signal C. The required system state can be achieved by assigning either A or B a value of logical 1. The state of the other input does not matter.

That condition is represented with the don't care value on B in Figure 10.12.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_586_0.png)

Now the output D is solely a function of the input C. We test by first applying a logical 0 and then a logical 1 to C and confirming the proper behavior for the signal D and indirectly partially confirming the correct operation of the output AND gate.

A and B are tested by reversing the roles. To test A, sensitize that path first by making C a logical 1 and then by making B a logical 0. Now the output D is solely a function of the input A. Testing B follows similarly, as reflected in Figure 10.13. As a side effect of the two test cases, the correct logical operation of the AND and OR gates is now confirmed.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_586_1.png)

Observe that six of the eight possible combinations of the three inputs are sufficient to confirm the proper logical operation of the circuit.

### 10.13.1.2 Debugging

Debugging or troubleshooting a fault in the circuit follows naturally. As noted, first hypothesize a stuck-at fault on signal D. The root cause of the problem can be either direct via a fault on the output or indirect via one of the inputs to the AND gate. To isolate the fault, choose the test vector that sensitizes path C as it is the simpler.

One must first confirm that the net A + B is in the logic 1 state. If not, pursue that path. Otherwise, the reasoning process proceeds as follows.

> > One knows how the output should behave if C is changed.
> > 
> > - If the desired changes are evident on D, move to the left and troubleshoot the A + B net.
> > - If the behavior of both of the AND gate inputs is correct, follow the D net.
> > - If AND gate input nets are not functioning properly, work backwards following the signal path that is not behaving properly.

### 10.13.2 Single Variable-Two Paths

In the logic circuits discussed earlier, the two paths are independent; that is, they do not share any common signals. At the next level of complexity the two paths share a common signal. Consider the configuration in Figure 10.14 as a simplified model of a more general circuit or system architecture.
