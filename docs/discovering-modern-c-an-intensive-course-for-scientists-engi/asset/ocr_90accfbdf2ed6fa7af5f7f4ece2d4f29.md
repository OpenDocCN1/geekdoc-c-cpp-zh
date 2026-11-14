# ### 3.3.2.3 Commonalities

When we are aiming for a common interface, we first have to ask ourselves: How similar are these two implementations of sum? At first glance not very:

+   - The values are accessed differently;
+   - The traversal of the entries is realized differently; and
+   - The termination criterion is different.

However, on a more abstract level, both functions perform the same tasks:

+   - Access of data
+   - Progress to the next entry
+   - Check for the end

The difference between the two implementations is how these tasks are realized with the given interfaces of the types. Thus, in order to provide a single generic function for both types, we have to establish a common interface.

# ### 3.3.2.4 Alternative Array Summation

In Section 3.3.2.1, we accessed the array in an index-oriented style that cannot be applied on lists arbitrarily dispersed in memory – at least not efficiently. Therefore, we reimplement the array summation here in a more sequential style with a stepwise traversal. We can achieve this by incrementing pointers until we pass the end of the array. The first address beyond the array is `a&[n]`, or more concisely with pointer arithmetic, `a + n`. Figure 3–1 illustrates that we start our traversal at the address of `a` and stop when we reach `a+n`. Thus, we specify the range of entries by a right-open interval of addresses.

When software is written for maximal applicability, right-open intervals turn out to be more versatile than closed intervals, especially for types like lists where positions are represented by memory addresses randomly allocated. The summation over a right-open interval can be implemented as shown in Listing 3–3.

```
Listing 3-3: Sum of array entries

template <typename T>
inline T accumulate_array(T* a, T* a_end)
{
    T sum(0);
    for (; a != a_end; ++a)
```

![](bbox=[0.375, 0.855, 0.655, 0.935])

Figure 3-1: An array of length n with begin and end pointers