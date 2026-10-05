# Chapter 6 Sorting

| | | |
| 0 | 0 | 0 |
| 1 | 1 | 1 |
| 2 | 2 | 2 |
| 7 | 4 | 3 |
| 4 | 5 | 4 |
| 5 | 6 | 5 |
| 6 | 3 | 6 |
| 7 | | 7 |
| 8 | | 8 |
| 9 | | 9 |

**Figure 6-4:** Improvements make bublesort faster, but it still has O(N²) performance.

After placing 7 after 3, the algorithm continues moving through the array and doesn't find any other items to swap so it knows that 7 and those that follow are in their final positions and don't need to be examined. If some item nearer to the top were larger than 7, the first pass would have swapped it past 7. In the middle image shown in Figure 6-4, the final items are shaded to indicate they don't need to be checked during later passes. The algorithm knows item 7 and the items after it are in their final positions, so it starts its second pass, moving upward through the array at the first item before 7, which swaps with items 6, 5, and 4, this time holding item 3 in a temporary variable until it reaches its final position.

Now item 3 and those that come before it in the array are in their final positions, so they are shaded in the last image in Figure 6-4.

The algorithm makes one final downward pass through the array, starting the pass at value 4 and ending at value 6. No swaps occur during this pass, so the algorithm ends.

These improvements make bubblesort faster. (In one test sorting 10,000 items, bubblesort would take 2.5 seconds without improvements and 0.69 seconds with improvements.) But it still has O(N²) performance, so there's a limit to the size of the list you can sort with bubblesort.

# O(n log N Algorithms

O(n log N) algorithms are much faster than O(N²), at least for larger arrays. if N is 1,000, N log N is less than 1x10⁴, but N² is roughly 100 times as big at 1x1⁶. That difference in speed makes these algorithms more useful in everyday programming, as for large arrays.