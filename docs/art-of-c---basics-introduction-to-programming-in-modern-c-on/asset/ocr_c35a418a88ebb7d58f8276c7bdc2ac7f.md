# 13.2. Code Reading - Generic Bubble Sort

> Haskell, for instance, has a concept of "Typeclass" to group/specify a set of related types. The "more modern" imperative languages like Rust and Swift also include the similar concepts like Trait and Protocol. They are slightly different, and slightly more general, than C#'s interface-based type constraints. The interested readers are encouraged to explore more from other resources on this topic.

The sample code in this lesson demonstrates one way to create a generic method over all numeric types (and, possibly more).

This is a demonstration that it *can* be done, but not necessarily that it should be done this way. This sample code, along with all code samples in this book, is primarily used to illustrate the features of the C# programming language.

Let's start from the main driver. This example main program creates an array of integers, and then it calls `Bubble.Sort()` to sort the numbers in the array according to their distances from a preset anchor point, `pivot == 20`.

As indicated, we implement our "sort according to the distance" method using generics. In particular, across all different numeric types. That is, even if we use an array of doubles, for instance, the method should work.

But, first let's take a look at a non-generic version of the implementation, especially, for an integer array. The compiler will use the generic template that we present in this lesson to generate something similar when the method is specialized for T being `int`.