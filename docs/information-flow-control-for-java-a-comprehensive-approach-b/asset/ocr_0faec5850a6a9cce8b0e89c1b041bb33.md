# Chapter 8

# Conclusion

This thesis presented several algorithms for precise analysis of programs in realistic programming languages like Java or C. It extends program dependence graphs to all features of Java bytecode, most prominently method parameters with nested field structures. In contrast to other slicers for Java, our system generates a system dependence graph, for which the standard two-phase context slicing algorithms can be leveraged.

For multi-threaded Java, we defined a precise approximation of interference dependence (with respect to the presented undecidability results), which arises when a shared variable is defined in one thread and used in another thread. Based on the Java memory model, our definition leverages points-to-information, which improves precision compared to previous definitions based on type or escape information.

When the binary information, whether one statement might influence another given is not sufficient, path conditions yield the detailed circumstances of the influence and can even eliminate false positives. This thesis shows that for object-oriented we constructs one detailed information on variable to gain conditions for automatic constraint solvers, and allow precise conditions for all object-oriented features. Furthermore, dynamic data allows a "flight recorder" and improves the precision of path data for a specific program execution.

The main contribution of this work is a novel approach for information flow control based on system dependence graph as defined in this thesis. The flows-sensitivity, context-sensitivity, and object-sensitivity of our slicer extends naturally to information flow control and exceeds the predominant approach for information flow control, namely security type systems.

The evaluation section showed that our new algorithm for information flow control dramatically reduced annotation burden compared to type systems, and its elevated evaluation. While it is clearly more expensive than security type systems, the evaluation demonstrates that security kernels are certified in reasonable time. As this certification process is only needed once at compile time, even an analysis that takes hours is acceptable when it guarantees security for