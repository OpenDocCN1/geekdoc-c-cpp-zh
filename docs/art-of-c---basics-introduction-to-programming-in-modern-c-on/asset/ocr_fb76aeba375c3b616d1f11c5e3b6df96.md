# # Lesson 20. Euclidean Distance

# ## 20.1. Introduction

C#'s new *record* class seems to provide the best of both worlds, value types and reference types. (Or, does it?)

We will again try using both *struct* and *record* (which is just *class* with special compiler support) for implementing data types.

The *rule of thumb* is to use *structs*, or *record structs*, for “pure” value or “small” data types and *records* for “large” data types.

> We often use the imprecise terms like “small” and “large” throughout this book. Unfortunately, the readers will have to develop certain “intuitions” through experience. These concepts are context-dependent, and they cannot be really precisely defined.

In this lesson, we will implement a small type “point” to represent a point in the two dimensional space. A point can be viewed as a pure value type, like a complex number, or as a data type, like a geographical coordinate, depending on the circumstances.

We also introduce the important concept of *interface* in this lesson. We will use a simple interface to provide a polymorphic behavior to the point types that we create using *struct* and *record* (class).

> The example that we use in this lesson seems to be a bit “contrived”. In practice, we will rarely define more than one types for the exactly same underlying concept in the same program. Nonetheless, this code sample illustrates an important use of interface in addition to demonstrating some essential uses of *struct* vs *record*.