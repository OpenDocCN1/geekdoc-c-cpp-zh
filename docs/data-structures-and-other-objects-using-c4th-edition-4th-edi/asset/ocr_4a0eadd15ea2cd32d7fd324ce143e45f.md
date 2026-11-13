# # Worst-Case Time for Serial Search
For an array of n elements, the worst-case time for serial search requires n array accesses.

With serial search, searches of an n-element array usually require fewer than n array accesses. Thus, the worst-case expression "n array accesses" makes serial search sound worse than it often is. An alternative is the average-case running time, which is obtained by averaging the running times for all different inputs of a particular kind. For example, we can develop an expression for the average-case running time of serial search based on all the targets that are actually in the array. To be concrete in this first example, suppose that the array has 10 elements, so that there are 10 possible targets. If we are searching for the target that occurs at the first location, then there is just one array access. If we are searching for the target that occurs at the second location, then there are two array accesses. And so on, through the final target, which requires 10 array accesses. In all, there are 10 possible targets, which require 1, 2, 3, 4, 5, 6, 7, 8, 9, or 10 array accesses. The average of all these searches is

\(\frac{1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10}{10} = 5.5\)

# FIGURE 12.1 Serial Search Algorithm

# ## Pseudocode for Serial Search

```
// Searches for a desired item in the n array elements starting at a[first]

Set a size_t variable i to 0, and set a boolean variable found to false.

while ((i < n) && !found)
{
    if (a[first+i] is the desired item)
        found = true;
    else
        ++i;
}

if (found)
    The desired item is in a[first+i].
else
    The desired item does not appear in the n items starting at a[first].
```