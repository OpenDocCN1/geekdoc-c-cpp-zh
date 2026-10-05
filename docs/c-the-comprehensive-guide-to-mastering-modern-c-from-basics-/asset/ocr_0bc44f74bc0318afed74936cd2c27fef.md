# 25.1 Algorithms

What is an algorithm in the context of the standard library? The classical algorithms are each a function template. In a broader sense, the new views are also algorithms. This function or class does something useful, and what it does, it does in a very general—generic—way. The fact that the algorithm functions and views are actually templates is precisely because they are meant to work generically: they should work on as many sequences as possible with as many element types as possible.

Every algorithm must be well-documented in its behavior. You need to be able to read the documentation and know exactly how the algorithm behaves when working with your data. And if it does something harmful, such as consuming too much memory or running too long, this case must also be described in the documentation.

If you need to solve a problem that is already solved or can be easily solved with <algorithm> or <numeric> or <ranges>, then you should use them:

+   * The functions and classes are tested by many programmers and are continuously maintained.

+   * The algorithms and range adapters are building blocks that you can assemble into complex tasks.

+   * It is therefore easier to write code with building blocks.

+   * Code made from building blocks is easier to debug.