![](bbox=[0.3, 0.095, 0.7, 0.37])

**Figure 1.15** Find the *largest* among five integers

# ## Algorithm Generalization

The algorithm shown in Figure 1.15 does not quite solve our original problem definition because it only handles five numbers. To make it work for all number series, we need to replace steps 2 through 5 to process an undetermined number of values. This requires that we generalize the statements so that they are the same. We can do this with a minor rephrasing of the statements as shown below.

> > **If the current number is greater than *largest*, set *largest* to the current number.**

We then include the rephrased statement in a repeat statement that executes the steps until all numbers are processed. The resulting algorithm is shown in Figure 1.16.

It is important to realize that the design is done *before* we write the program. In this respect, it is like the architect's blueprint. No one would start to build a house without a detailed set of plans, yet one of the most common errors of both experienced and new

![](bbox=[0.3, 0.685, 0.64, 0.885])

**Figure 1.16** Algorithm to find *largest* among *n* numbers