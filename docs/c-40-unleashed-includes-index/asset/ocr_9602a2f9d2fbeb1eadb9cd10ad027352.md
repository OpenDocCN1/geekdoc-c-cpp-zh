Notice we're passing an IEnumerable<Apple> object where IEnumerable<Fruit> is expected. Intuitively, you might say this should be fine because every Apple is a Fruit. It turns out that this is safe, but before .NET 4, the compiler would reject this code because it treated IEnumerable<> as invariant. What this means will become clear in a just a moment. For now, just take a look at Figure 15.33.

![](bbox=[0.075, 0.206, 0.586, 0.41])

**FIGURE 15.33** Before .NET 4, IEnumerable<T> was invariant in T.

To understand why this code got rejected before C# 4.0, we need to take a tour through the wonderful world of variance. While variance is deeply rooted in (scary sounding) category theory and type theory, it has become an everyday concept now in the world of .NET programming. This is not only the case for generic types but also for delegates, as you will see during our coverage of delegates in Chapter 17.

In a nutshell, generic variance annotations relate subtyping on constructed types with subtyping on the type arguments used to construct the type. For example, if we know that every Apple is a Fruit, we can also say that every IEnumerable of Apple objects can be treated safely as an IEnumerable of Fruit? The word safety is essential in this definition because type safety is at stake. (The following section illustrates the dangers that come from broken variance treatment.)

# ## Broken Covariance for Array Types

Since the .NET Framework was released, arrays have been covariant. Going back to our definition of variance annotations, there was a mention of “constructed types.” Array types are such animals because any element type can be used to construct an array type. For example, given the type int, we can construct an array that can hold integer values (that is, which is of type int[]). And this by itself is a new type we can create an array type out of, namely a jagged int[][] array.

Our next duty is to express a subtyping relationship between array types based on the knowledge of a subtyping relationship between the element types. For example, if we