![](bbox=[0.034, 0.079, 0.785, 0.514])

FIGURE 20.9  Types of join operations compared.

# Aggregate

The aggregate operator takes a sequence of elements of type T and turns them into a single value of another type A, which stands for accumulated or aggregated depending on your choice of vocab. But how can we transform any number of elements of type T into a single value of another type? Let’s start with the simplest case where both types are the same and look at how we would create the sum of a sequence of integer values, as illustrated in Figure 20.10.

Based on this, we can see we don’t need any fancy stuff to compute the sum of an unknown number of integer values: All we need is a binary function that can add two numbers. By reusing this function repeatedly, consuming one element in the input sequence at a time (in a left-to-right fashion), we can compute the sum.

So far, we’ve stayed in the same domain of values for our input sequence and the result of the aggregation, but in a more generalized world we want those types to differ. In fact, for a sum we might want the sum of integer values to result in a long, to reduce the chance of overflowing the 32-bit precision. More generally, we might want to do things like aggregating a sequence of numbers into a string concatenating them. In that case it’s clear the input type (a sequence of integers) differs from the aggregated output type (a single string).