# Solutions to Chapter 9 | Sorting and Searching

9.7 A circus is designing a tower routine consisting of people standing atop another's shoulders. For practical and aesthetic reasons, each person must be both shorter and lighter than the person below him or her. Given the heights and weights of each person in the circus, write a method to compute the largest possible number of people in such a tower.

EXAMPLE:

Input (ht, wt): (66, 100) (70, 150) (56, 90) (70, 190) (60, 95) (68, 110)

Output: The longest tower is length 6 and from top to bottom: (56, 90) (60, 95) (66, 100) (68, 110) (70, 150) (75, 190)

pg 66

# SOLUTION

Step 1. Sort all items by height first, and then by weight. This means that if all the heights are unique, then the items will be sorted by their height. If heights are the same, items will be sorted by their weight.

Example:

+   Before sorting: (60, 100) (70, 150) (56, 90) (75, 190) (60, 95) (68, 110).

+   After sorting: (56, 90), (60, 95), (60, 100), (68, 110), (70, 150), (75, 190).

Step 2. Find the longest sequence which contains increasing heights and increasing weights.

To do this, we:

+   a) Start at the beginning of the sequence. Currently, max_sequence is empty.

+   b) If, for the next item, the height and the weight is not greater than those of the previous item, we mark this item as "unfit".

| (60,95) | (65,100) | (75,80) | (80,100) |
| | | (unfit item) | |

c) If the sequence found has more items than "max sequence", it becomes "max sequence".
d) After that the search is repeated from the "unfit item", until we reach the end of the original sequence.

```
public class Question {
  ArrayList<Htwt> items;
  ArrayList<Htwt> lastFoundSeq;
  ArrayList<Htwt> maxSeq;
```