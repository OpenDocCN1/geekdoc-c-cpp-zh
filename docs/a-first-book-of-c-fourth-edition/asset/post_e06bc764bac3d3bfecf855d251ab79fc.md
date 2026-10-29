
Find the smallest element from the current element being referenced to the last element by:

- Setting the minimum value equal to the current element
- Saving (storing) the index of the current element
- For each element in the list, from the current element + 1 to the last element in the list
- If element[inner loop index] < minimum value
- Set the minimum value = element[inner loop index]
- Save the index of the newfound minimum value
- EndIf
- EndFor
- Swap the current value with the new minimum value
- Increment the exchange count
- EndFor
- Return the exchange count

The selectionSort() function incorporates this procedure into a C++ function:

```
int selectionSort(int num[], int numel)
{
    int i, j, min, minidx, temp, moves = 0;

    for ( i = 0; i < (numel - 1); i++)
    {
        min = num[i];    // assume minimum is the first array element
        minidx = i;      // index of minimum element
        for(j = i + 1; j < numel; j++)
        {
            if (num[j] < min)    // if you've located a lower value
            {                   // capture it
                min = num[j];
                minidx = j;
            }
        }
        if (min < num[i])    // check whether you have a new minimum
        {                   // and if you do, swap values
            temp = num[i];
            num[i] = min;
            num[minidx] = temp;
            moves++;
        }
    }

    return moves;
}
```

The selectionSort() function expects two arguments: the list to be sorted and the number of elements in the list. As the pseudocode specifies, a nested set of for loops performs the sort. The outer for loop causes one less pass through the list than the total number of items in the list. For each pass, the variable min is initially assigned the value num[i], where i is the outer for loop's counter variable. Because i begins at 0 and ends at 1 less than numel, each element in the list, except the last, is successively designated as the current element.

The inner loop cycles through the elements below the current element and is used to select the next smallest value. Therefore, this loop begins at the index value i + 1 and continues through the end of the list. When a new minimum is found, its value and position in the list are stored in the variables min and minIdx. At completion of the inner loop, an exchange is made only if a value less than that in the current position is found.

Program 7.11 was constructed to test selectionSort(). This program implements a selection sort for the same list of 10 numbers used previously to test search algorithms. For later comparison to other sorting algorithms, the number of actual moves the program makes to get data into sorted order is counted and displayed.

## Program 7.11

```
#include <iostream>
using namespace std;

int selectionSort(int [], int);
int main()
{
const int NUMEL = 10;
int nums[NUMEL] = {22,5,67,98,45,32,101,99,73,10};
int i, moves;

moves = selectionSort(nums, NUMEL);

cout << "The sorted list, in ascending order, is:\n";
for (i = 0; i < NUMEL; i++)
    cout << " " << nums[i];

cout << '\n' << moves << " moves were made to sort this list\n";

return 0;
}
int selectionSort(int num[], int numel)
{
int i, j, min, minIdx, temp, moves = 0;

for ( i = 0; i < (numel - 1); i++)
```

```
{ min = num[i]; // assume minimum is the first array element minidx = i; // index of minimum element for(j = i + 1; j < numel; j++) { if (num[j] < min) // if you've located a lower value { // capture it min = num[j]; minidx = j; } } if (min < num[i]) // check whether you have a new minimum { // and if you do, swap values temp = num[i]; num[i] = min; num[minidx] = temp; moves++; } } return moves; }
```

The output Program 7.11 produces is as follows:

```
The sorted list, in ascending order, is: 5 10 22 32 45 67 73 98 99 101 8 moves were made to sort this list
```

Clearly, the number of moves displayed depends on the initial order of values in the list. An advantage of the selection sort is that the maximum number of moves that must be made is n - 1, where n is the number of items in the list. Further, each move is a final move that results in an element residing in its final location in the sorted list.

A disadvantage of the selection sort is that n(n - 1) / 2 comparisons are always required, regardless of the initial arrangement of data. This number of comparisons is obtained as follows: The last pass always requires one comparison, the next-to-last pass requires two comparisons, and so on up to the first pass, which requires n - 1 comparisons. Therefore, the total number of comparisons is the following:

1 + 2 + 3 + ... + n - 1 = n(n - 1) / 2 = n² / 2 - n / 2

For large values of n, the n² dominates, and the order of the selection sort is O(n²).

## Exchange (Bubble) Sort

In an exchange sort, adjacent elements of the list are exchanged with one another so that the list becomes sorted. One example of this sequence of exchanges is the bubble sort, in which successive values in the list are compared, beginning with the first two elements. If the list is to be sorted in ascending (from smallest to largest) order, the

smaller value of the two being compared is always placed before the larger value. For lists sorted in descending (from largest to smallest) order, the smaller of the two values being compared is always placed after the larger value.

For example, a list of values is to be sorted in ascending order. If the first element in the list is larger than the second, the two elements are exchanged. Then the second and third elements are compared. Again, if the second element is larger than the third, these two elements are exchanged. This process continues until the last two elements have been compared and exchanged, if necessary. If no exchanges were made during this initial pass through the data, the data is in the correct order and the process is finished; otherwise, a second pass is made through the data, starting from the first element and stopping at the next-to-last element. The reason for stopping at the next-to-last element on the second pass is that the first pass always results in the most positive value "sinking" to the bottom of the list.

To see a specific example, examine the list of numbers in Figure 7.13. The first comparison results in exchanging the first two element values, 690 and 307. The next comparison, between elements two and three in the revised list, results in exchanging values between the second and third elements, 690 and 32. This comparison and possible switching of adjacent values continues until the last two elements have been compared and possibly exchanged. This process completes the first pass through the data and results in the largest number moving to the bottom of the list. As the largest value sinks to the bottom of the list, the smaller elements slowly rise, or "bubble," to the top of the list. This bubbling effect of the smaller elements is what gave rise to the name "bubble sort" for this sorting algorithm.

| 690 ↔ | 307 | 307 | 307 | 307 |
| 307 ↔ | 690 ↔ | 32 | 32 | 32 |
| 32 | 32 ↔ | 690 ↔ | 155 | 155 |
| 155 | 155 | 155 ↔ | 690 ↔ | 426 |
| 426 | 426 | 426 | 426 ↔ | 690 |

### Figure 7.13 The first pass of an exchange sort

Because the first pass through the list ensures that the largest value always moves to the bottom of the list, the second pass stops at the next-to-last element. This process continues with each pass stopping at one higher element than the previous pass, until n - 1 passes through the list have been completed or no exchanges are necessary in any single pass. In both cases, the resulting list is in sorted order. The pseudocode describing this sort is as follows:

```
Set exchange count to 0 (not required, but done to keep track of the exchanges)
For the first element in the list to 1 less than the last element (i index)
For the second element in the list to the last element (j index)
If num[j] < num[j - 1]
{
Swap num[j] with num[j - 1]
increment exchange count
}
```
