The set of input and corresponding output signals combined with the order in which they are applied form the basis for the test cases in the test procedure. While mainly informal during early testing and debugging, the set is called and formalized during the later phases of the design cycle.

As the process now unfolds, we will look first at testing and debugging of combinational logic and then at sequential logic. But first we will have a short digression.

# 10.11.4 Sudden Failure during Debugging

Let's now assume that we have been working on the circuit for some time and have been approaching debugging and integration tasks methodically, adding and debugging one functional subcomponent at a time. So far, three of the five modules in the system have been debugged and integrated, and now the fourth is added. The new module does not work (although it worked as a stand-alone component). Furthermore, the first three modules now fail to work properly. If module 4 is disconnected from the circuit, the original components once again work properly. Repeated tests on module 4 alone fail to identify any possible faults. What could the problem be?

Consider a simple model. A Thévenin equivalent circuit can be developed for each of the five components in the system. As each one is integrated, the system can be modeled as in the sequence of drawings shown in Figure 10.8.

![](bbox=[0.25, 0.425, 0.85, 0.58])

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