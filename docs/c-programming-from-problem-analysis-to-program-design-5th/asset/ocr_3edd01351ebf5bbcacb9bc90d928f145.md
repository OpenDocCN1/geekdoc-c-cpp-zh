container in terms of the members of a specific class. All those algorithms and a few more are also available in a more general form, called **generic algorithms**, and can be applied in a variety of situations. This section discusses some of these generic algorithms.

The STL contains algorithms that look only at the elements in a container and that move the elements of a container. It also has algorithms that can perform a specific calculation, such as finding the sum of the elements of a numeric container. The STL also contains algorithms for basic set theory operations, such as set union and intersection. You have already encountered some of the generic algorithms, such as the copy algorithm, which copies the elements from a given range of elements to another place, such as another container or the screen. The algorithms in the STL can be classified into the following categories:

+   - Nonomodifying algorithms
+   - Modifying algorithms
+   - Numeric algorithms
+   - STL algorithms

The next four sections describe these algorithms. Most of the generic algorithms are contained in the header file algorithm. Certain algorithms, such as numeric, are contained in the header file numeric.

# NONMODIFYING ALGORITHMS

Nonmodifying algorithms do not modify the elements of the container; they only investigate the elements. Table H-13 describes the nonmodifying algorithms.

**TABLE H-13 — Nonmodifying Algorithms**

| Nonmodifying Algorithms |  |  |
|---|---|---|
| `adjacent_find` | `find_if` | `max` |
| `binary_search` | `find_end` | `max_element` |
| `count` | `find_first_of` | `min` |
| `count_if` | `for_each` | `min_element` |
| `equal` | `includes` | `search` |
| `equal_range` | `lower_bound` | `search_n` |
| `find` | `mismatch` | `upper_bound` |