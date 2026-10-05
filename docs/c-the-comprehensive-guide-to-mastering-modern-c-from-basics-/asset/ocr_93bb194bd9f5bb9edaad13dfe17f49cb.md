# 25.4 Algorithms of the Standard Library

All algorithms, ranges, and views in the context of this chapter are function templates or classes from the <algorithm> and <ranges> headers. Some come from <numeric>, which I will mention separately. Typically, algorithms work together with containers and use iterators as means. This, in turn, results in algorithms also working with streams, as they also offer iterators.

The fact that all algorithms are implemented as templates means that the code of the algorithm can automatically be used by the compiler as inline on the spot. Unlike with object hierarchies with potentially virtual methods that prevent inlining, this provides as much performance as one can possibly get. For the algorithms of the standard library, maximum speed within the scope of their general implementation is one of the top design principles.

![](bbox=[0.257, 0.689, 0.742, 0.766])

**Figure 25.1** The containers do not work directly with the algorithms but “communicate” with them through iterators.