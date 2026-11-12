```
```cpp
6 int main()
7 {
8     std::array<int, 8> a
9         {-2, -3, 4, -1, -2, 1, 5, -3};
10
11     std::cout << kadaneld(a.cbegin(), a.cend())
12               << std::endl;
13
14     std::vector<int> v
15         {-1, 4, -2, 5, -5, 2, -20, 6};
16
17     std::cout << kadaneld(v.cbegin(), v.cend())
18               << std::endl;
19
20     std::forward_list<int> l
21         {-2, 1, -3, 4, -1, 2, 1, -5, 4};
22
23     std::cout << kadaneld(l.cbegin(), l.cend())
24               << std::endl;
25
26 }
```
```

It prints

```
```
7
7
6
```
```

# ## Find indices of max subarray

# ### Problem

Design and implement an efficient program to find a contiguous subarray within a one-dimensional array of integers which has the largest sum. The result should include sum and (start, end) of the subarray.

It is easy to see that

+   - the maximum subarray starts and ends in positive elements
+   - if we start from the first positive element, i.e., a[l], and sum over the subsequent elements until the sum drops negative at a[r], then the optimal subarray is either
+     - in a[l..r] and starts from a[l], or
+     - in a[r + 1..n].