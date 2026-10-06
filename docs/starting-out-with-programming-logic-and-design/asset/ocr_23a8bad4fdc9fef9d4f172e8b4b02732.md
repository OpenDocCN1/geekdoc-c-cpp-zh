# Figure 9-25 Flowchart for the binarySearch function

| binarySearch \
| (Integer array[], \
| Integer value,
| Integer arraySize) |

| Declare first = 0 \
| Declare last = arraySize - 1 \
| Declare position = -1 \
| Declare Boolean found = False \
| Declare Integer middle |

![](bbox=[0.193, 0.275, 0.804, 0.673])

# Efficiency of a Binary Search

Obviously, a binary search is much more efficient than a sequential search. Every time a binary search makes a comparison and fails to find the desired item, it eliminates half of the remaining portion of the array that must be searched. For example, consider an array with 1000 elements. If a binary search fails to find an item on the first attempt, on the second attempt, the number of elements that remains to be searched is 500. If the item is not found this process continues until the binary search has either located the desired item or determined that it is not in the array. With 1000 elements this takes no more than 10 comparisons. (Compare this to a sequential search, which would make an average of 500 comparisons!)