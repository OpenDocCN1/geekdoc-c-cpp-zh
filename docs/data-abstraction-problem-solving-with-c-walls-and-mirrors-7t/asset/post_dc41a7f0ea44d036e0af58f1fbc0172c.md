
FIGURE 11-1 A selection sort of an array of five integers

Gray elements are selected; blue elements comprise the sorted portion of the array.

| Step | Array |
| :--- | :--- |
| Initial array: | 29 10 14 37 13 |
| After 1st swap: | 29 10 14 13 37 |
| After 2nd swap: | 13 10 14 29 37 |
| After 3rd swap: | 13 10 14 29 37 |
| After 4th swap: | 10 13 14 29 37 |

Question 1 Trace the selection sort as it sorts the following array into ascending order: 20 80 40 25 60 30

Question 2 Repeat the previous question, but instead sort the array into descending order.

Listing 11-1 gives a C++ function, and the two functions it calls, that performs a selection sort on an array theArray of n items, assuming that ItemType is the data type of the array's entries.

```
LISTING 11-1 An implementation of the selection sort

/* Finds the largest item in an array.
// Pre: The size of the array is >= 1.
// Post: The arguments are unchanged.
// param theArray The given array.
// param Size The number of elements in theArray.
// Return: The index of the largest entry in the array. */
int findIndexOfLargest(const ItemType theArray[], int size);

/* Sorts the items in an array into ascending order.
// Pre: None.
// Post: The array is sorted into ascending order; the size of the array
//       is unchanged.
// param theArray The array to sort.
// param n The size of theArray. */
void selectionSort(ItemType theArray[], int n)
{   // last = index of the last item in the subarray of items yet
    //       to be sorted;
    // largest = index of the largest item found
    for (int last = n - 1; last > 0; last--)
    {
        // At this point, theArray[last+1..n-1] is sorted, and its
        // entries are greater than those in theArray[0..last].
        // Select the largest entry in theArray[0..last]
        int largest = findIndexOfLargest(theArray, last+1);

        // Swap the largest entry, theArray[largest], with
        // theArray[last]
        std::swap(theArray[largest], theArray[last]);
    } // end for
} // end selectionSort

int findIndexOfLargest(const ItemType theArray[], int size)
{
    int indexSoFar = 0; // Index of largest entry found so far
    for (int currentIndex = 1; currentIndex < size; currentIndex++)
    {
        // At this point, theArray[indexSoFar] >= all entries in
        // theArray[0..currentIndex - 1]
        if (theArray[currentIndex] > theArray[indexSoFar])
            indexSoFar = currentIndex;
    } // end for

    return indexSoFar; // Index of largest entry
} // end findIndexOfLargest
```

Analysis. As you can see from the previous algorithm, sorting in general compares, exchanges, or moves items. As a first step in analyzing such algorithms, you should count these operations. Generally, such operations are more expensive than ones that control loops or manipulate array indexes, particularly when the data to be sorted is more complex than integers or characters. Thus, our approach ignores these incidental operations. You should convince yourself that by ignoring such operations we do not affect our final result. (See Exercise 1.)

Clearly, the for loop in the function selectionSort executes n - 1 times. Thus, selectionSort calls each of the functions findIndexOfLargest and swap n - 1 times. Each call to findIndexOfLargest causes its loop to execute last times (that is, size - 1 times when size is last + 1). Thus, the n - 1 calls to findIndexOfLargest, for values of last that range from n - 1 down to 1, cause the loop in findIndexOfLargest to execute a total of

(n - 1) + (n - 2) + ... + 1 = n x (n - 1)/2

times. Because each execution of findIndexOfLargest's loop performs one comparison, the calls to findIndexOfLargest require

n x (n - 1)/2

comparisons.

The n - 1 calls to swap result in n - 1 exchanges. Each exchange requires three assignments, or data moves. Thus, the calls to swap require

3 x (n - 1)

moves.

Together, a selection sort of $n$ items requires

\( n \times (n - 1) / 2 + 3 \times (n - 1) = n^2/2 + 5 \times n / 2 - 3 \)

major operations. By applying the properties of the growth-rate functions given in Chapter 10, you can ignore low-order terms to get \( O(n^2 / 2) \) and then ignore the multiplier 1/2 to get \( O(n^2) \). Thus, the selection sort is \( O(n^2) \).

Selection sort is \( O(n^2) \)

Although a selection sort does not depend on the initial arrangement of the data, which is an advantage of this algorithm, it is appropriate only for small \( n \) because \( O(n^2) \) grows rapidly. While the algorithm requires \( O(n^2) \) comparisons, it requires only \( O(n) \) data moves. A selection sort could be a good choice over other approaches when data moves are costly but comparisons are not. Such might be the case if each data item is lengthy but the sort key is short.

> Note: If you are sorting a very large array, an \( O(n^2) \) algorithm is probably too inefficient to use.

### 11.1.2 The Bubble Sort

The next sorting algorithm is one that you may have seen already. The **bubble sort** compares adjacent items and exchanges them if they are out of order. This sort usually requires several passes over the data. During the first pass, you compare the first two items in the array. If they are out of order, you exchange them. You then compare the items in the next pair—that is, in positions 2 and 3 of the array. If they are out of order, you exchange them. You proceed in the same manner, comparing and exchanging items two at a time, until you reach the end of the array.

Figure 11-2a illustrates the first pass of a bubble sort of an array of five integers. You compare the items in the first pair—29 and 10—and exchange them because they are out of order. Next you consider the second pair—29 and 14—and exchange these items because they are out of order. The items in the third pair—29 and 37—are in order, and so you do not exchange them. Finally, you exchange the items in the last pair—37 and 13.

When you order successive pairs of items, the largest item bubbles to the top (end) of the array

Although the array is not sorted after the first pass, the largest item has “bubbled” to its proper position at the end of the array. During the second pass of the bubble sort, you return to the beginning of the array and consider pairs of items in exactly the same manner as the first pass. You do not, however, include the last—and largest—item of the array. That is, the second pass considers the first n – 1 items of the array. After the second pass, the second-largest item in the array will be in its proper place in the next-to-last position of the array, as Figure 11-2b illustrates. Now, ignoring the last two items, which are in order, you continue with subsequent passes until the array is sorted.

FIGURE 11-2 The first two passes of a bubble sort of an array of five integers

| (a) Pass 1 | (b) Pass 2 |
| :--- | :--- |
| Initial array: 29 10 14 37 13 | |
| 10 29 14 37 13 | 10 14 29 13 37 |
| 10 14 29 37 13 | 10 14 29 13 37 |
| 10 14 29 37 13 | 10 14 29 13 37 |
| 10 14 29 13 37 | 10 14 13 29 37 |
| 10 14 29 13 37 | 10 14 13 29 37 |

The bubble sort usually requires several passes through the array until the array is sorted.

Although a bubble sort requires at most n – 1 passes to sort the array, fewer passes might be possible to sort a particular array. Thus, you could terminate the process if no exchanges occur during any pass. The following C++ function bubbleSort uses a boolean variable to signal when an exchange occurs during a particular pass. The function uses the previous swap function.

LISTING 11-2 An implementation of the bubble sort

```
void bubbleSort(ItemType theArray[], int n)
{
   bool sorted = false;   // False when swaps occur
   int pass = 1;
   while ((!sorted) && (pass < n))
   {
      // At this point, theArray[n+1-pass..n-1] is sorted
      //     and all of its entries are > the entries in theArray[0..n-pass]
      sorted = true;       // Assume sorted
      for (int index = 0; index < n - pass; index++)
      {
         // At this point, all entries in theArray[0..index-1]
         //     are < theArray[index]
         int nextIndex = index + 1;
         if (theArray[index] > theArray[nextIndex])
         {
            // Exchange entries
            std::swap(theArray[index], theArray[nextIndex]);
            sorted = false;   // Signal exchange
         }  // end if
      }  // end for
      // Assertion: theArray[0..n-pass-1] < theArray[n-pass]
      pass++;
   }  // end while
}  // end bubbleSort
```

Question 3 Trace the bubble sort as it sorts the following array into ascending order: 25 30 20 80 40 60.

Question 4 Repeat the previous question, but instead sort the array into descending order.
