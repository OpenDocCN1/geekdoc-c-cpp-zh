parameters come in pairs of iterators—namely, begin and end.

Ranges are the successors of these iterator pairs and, together with views, they extend the algorithms. All algorithms from std that takes pairs of iterators can now be found in std::ranges with ranges as parameters—the standard then calls them constrained algorithms. I find the name misleading because the algorithms in std::ranges are not restrictive at all, but rather extended:

+   - They accept ranges as parameters but also work with pairs of iterators.

+   - They typically return ranges, so they can be directly combined with views.

+   - They consistently support an optional projection parameter, which allows access to the range elements using a functor—for example, by specifying a member function.

You can therefore expect that range algorithms will be extended sooner than classical algorithms. This is already the case. For example, ranges::starts_with() no longer has a counterpart in std. I mentioned in the previous chapter on containers what algorithms and ranges are because they go hand in hand. Algorithms, ranges, and views from the <algorithm>, <numeric>, and <ranges> headers mostly work with containers. You can also write your own algorithms and views.

In this chapter, I will try to familiarize you with algorithms, ranges, and views. When I speak of algorithm, I usually mean functions from <algorithm> in