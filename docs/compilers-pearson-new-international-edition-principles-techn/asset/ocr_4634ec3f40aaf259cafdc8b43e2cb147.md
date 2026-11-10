![](bbox=[0.321, 0.177, 0.678, 0.433])

Figure 9.29: Meet of UNDEF and a constant

uninitialized along any path to a point where it is used. How would you modify the framework of this section to detect such situations?

# **Exercise 9.4.2:**

An interesting and powerful data-flow-analysis framework is obtained by imagining the domain V to be all possible partitions of expressions, so that the two expressions are in the same class if and only if they are certain to have the same value along any path to the point in question. To avoid having to list an infinity of expressions, we can represent V by listing only the minimal pairs of equivalent expressions. For example, if we execute the statements

```
a = b
c = a + d
```

then the minimal set of equivalences is {a = b, c ≡ a + d}. From these follow other equivalences, such as c ≡ b + d and a + e ≡ b + e, but there is no need to list these explicitly.

+   a) What is the appropriate meet operator for this framework?
+   
+   b) Give a data structure to represent domain values and an algorithm to implement the meet operator.
+   
+   c) What are the appropriate functions to associate with statements? Explain the effect that a statement such as a = b+c should have on a partition of expressions (i.e., on a value in V).
+   
+   d) Is this framework monotone? Distributive?