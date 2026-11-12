```
```cpp
}

template <size_t Index, class ElementType, size_t N>
inline const ElementType&
get(const array<ElementType, N>& a)
{
    static_assert(Index < N, "Index out_of_bounds in std::get<> (const std::array&)");
    return a[Index];
}

template <size_t Index, class ElementType, size_t N>
inline ElementType&&
get(array<ElementType, N>&& a)
{
    static_assert(Index < N, "Index out_of_bounds in std::get<> (std::array&&)");
    return std::move(a[Index]);
}
```
```

# ## 1.10 Seating Problem

# ### Problem Description

GreedSox, a popular major-league baseball team, is interested in one thing: making money. They have hired you as a consultant to help boost their group ticket sales. They have noticed the following problem. When a group wants to see a ballgame, all members of the group need seats (in the bleacher section), or they go away. Since partial groups can't be seated, the bleachers are often not full. There is still space available, but not enough space for the entire group. In this case, the group cannot be seated, losing money for the GreedSox.

The GreedSox want your recommendation on a new seating policy. Instead of seating people first-come/first-serve, the GreedSox decide to seat large groups first, followed by smaller groups, and finally singles (i.e., groups of 1).

You are given a set of groups, G[1..m] = [g_1, g_2, ..., g_m], where g_i is a number representing the size of the group. Assume that the bleachers seat n people. Consider the following greedy seating algorithm, where the function ADMIT(i) admits group i, and REJECT(i) sends away group i.