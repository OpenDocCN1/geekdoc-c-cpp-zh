the binary search of order log₂n. Notationally, they’re expressed as O(n) and O(log₂n); the O is read as "the order of."

# Two Algorithms

Two major categories of sorting techniques, called internal and external sorts, are available for sorting data. Internal sorts are used when the data list isn’t too large and the complete list can be stored in the computer’s memory, usually in an array. External sorts are used for much larger data sets stored on external storage media and can’t be accommodated in the computer’s memory as a complete unit. Next, you learn about two internal sort algorithms that can be used when sorting lists with fewer than approximately 50 elements. For larger lists, more sophisticated sorting algorithms are typically used.

# Selection Sort

One of the simplest sorting techniques is the selection sort, in which the smallest value is selected from the complete list of data and exchanged with the first element in the list. After this first selection and exchange, the next smallest element in the revised list is selected and exchanged with the second element in the list. Because the smallest element is already in the first position in the list, this second pass needs to consider only the second through last elements. For a list consisting of n elements, this process is repeated n - 1 times, with each pass through the list requiring one less comparison than the previous pass.

For example, take a look at the list of numbers shown in Figure 7.12. The first pass through the initial list results in the number 32 being selected and exchanged with the first element in the list. The second pass, made on the reordered list, results in the number 155 being selected from the second through fifth elements. This value is then exchanged with the second element in the list. The third pass selects the number 307 from the third through fifth elements in the list and exchanges this value with the third element. Finally, the fourth and last pass through the list selects the remaining minimum value and exchanges it with the fourth list element. Although each pass in this example resulted in an exchange, no exchange would have been made in a pass if the smallest value were already in the correct location.

| Initial list | Pass 1 | Pass 2 | Pass 3 | Pass 4 |
|---|---|---|---|---|
| 690 | 32 | 32 | 32 | 32 |
| 307 | 307 | 155 | 144 | 144 |
| 32 | 690 | 690 | 307 | 307 |
| 155 | 155 | 307 | 690 | 426 |
| 426 | 426 | 426 | 426 | 690 |

Figure 7.12 A sample selection sort

In pseudocode, the selection sort is described as follows:

```
Set exchange count to 0 (not required, but done to keep track of the exchanges)
For each element in the list from first to next to last
```