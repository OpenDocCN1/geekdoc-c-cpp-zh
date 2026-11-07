
```c
printf("%s", "\n\nThe sorted array is");
printArray(answer); // output sorted array

// display median element
printf("\n\nThe median is element %u of\n"
"the sorted %u element array.\n"
"For this run the median is %u\n",
SIZE / 2, SIZE, answer[SIZE / 2]);
}

// determine most frequent response
void mode(int freq[], const int answer[]) {
printf("\n\n%5s %5s\n", "-------", " Mode", "-------");

// initialize frequencies to 0
for (size_t rating = 1; rating <= 9; ++rating) {
freq[rating] = 0;
}

// summarize frequencies
for (size_t j = 0; j < SIZE; ++j) {
++freq[answer[j]];
}

// output headers for result columns
printf("%s%11s%19s\n\n%5s%5s\n",
"Response", "Frequency", "Bar Chart",
"1 1 2 2", "5 0 5 0 5");

// output results
int largest = 0; // represents largest frequency
int modeValue = 0; // represents most frequent response
for (size_t rating = 1; rating <= 9; ++rating) {
printf("%8zu%11d ", rating, freq[rating]);

// keep track of mode value and largest frequency value
if (freq[rating] > largest) {
largest = freq[rating];
modeValue = rating;
}

// output bar representing frequency value
for (int h = 1; h <= freq[rating]; ++h) {
printf("%s", "*");
}

puts(""); // begin new line of output
}
}
```

// display the mode value
printf("\nThe mode is the most frequent value.\n" "For this run the mode is %d which occurred %d times.\n", modeValue, largest);
}
// function that sorts an array with bubble sort algorithm
void bubbleSort(int a[]) {
// loop to control number of passes
for (int pass = 1; pass < SIZE; ++pass) {
// loop to control number of comparisons per pass
for (size_t j = 0; j < SIZE - 1; ++j) {
// swap elements if out of order
if (a[j] > a[j + 1]) {
int hold = a[j];
a[j] = a[j + 1];
a[j + 1] = hold;
}
}
}
}
// output array contents (20 values per row)
void printArray(const int a[]) {
// output array contents
for (size_t j = 0; j < SIZE; ++j) {
if (j % 20 == 0) { // begin new line every 20 values
puts("");
}
printf("%2d", a[j]);
}
}

## Mean
The mean is the average value of the data items. The mean is equal to the total of all the data items divided by the number of data items (99). The mean value for this run is: 681 / 99 = 6.8788

## Median
The unsorted array of responses is
6 7 8 9 8 7 8 9 8 9 7 8 9 5 9 8 7 8 7 8
6 7 8 9 3 9 8 7 8 7 7 8 9 8 9 8 9 7 8 9

## Mode
The mode is the value that occurs most frequently among the 99 responses. Function mode (lines 76–119) determines the mode by counting the number of responses of each type, then selecting the value with the greatest count. This version of function mode does not handle a tie (see Exercise 6.14). Function mode also produces a bar chart to aid in determining the mode graphically.

## Related Exercises
This case study is supported by the following exercise:

- Exercise 6.14 (Mean, Median and Mode Program Modifications).

## Self Check
1 (Multiple Choice) Which of the following statements a), b) or c) is false?

- a) The median is the middle value among the sorted data items.
- b) The algorithm for finding the median of the values in an array sorts the array into ascending order, then picks the sorted array's middle element.
- c) When the number of elements is even, the median is calculated as the mean of the two middle elements.
- d) All of the above statements are true.

Answer: d.

2 (Multiple Choice) Which of the following statements is a), b) or c) is false?

- a) The mode is the value that occurs most frequently among the data items.
- b) The algorithm for finding the mode counts the number of occurrences of each value, then selects the most frequently occurring value. One problem with determining the mode is what to do in case of a tie.
- c) The mode can be determined visually by graphing the frequencies of the values in a bar chart—the longest bar represents the mode.
- d) All of the above statements are true.

Answer: d.

## 6.10 Searching Arrays
You'll often work with large amounts of data stored in arrays. It may be necessary to determine whether an array contains a value that matches a certain key value. The process of finding a key value in an array is called searching. This section discusses two searching techniques—the simple linear search technique and the more efficient (but more complicated) binary search technique. Exercises 6.32 and 6.33 ask you to implement recursive versions of the linear search and the binary search.

### 6.10.1 Searching an Array with Linear Search
A linear search (Fig. 6.14, lines 37–46) compares each array element with the search key. The array is not sorted, so it's just as likely the value will be found in the first element as in the last. On average, therefore, the program will have to compare the
search key with half the array elements. If the key value is found, we return the element's subscript; otherwise, we return -1 (an invalid subscript).

```c
// fig06_14.c
// Linear search of an array.
#include <stdio.h>
#define SIZE 100

// function prototype
int linearSearch(const int array[], int key, size_t size);

// function main begins program execution
int main(void) {
    int a[SIZE] = {0}; // create array a

    // create some data
    for (size_t x = 0; x < SIZE; ++x) {
        a[x] = 2 ^ x;
    }

    printf("Enter integer search key: ");
    int searchKey = 0; // value to locate in array a
    scanf("%d", &searchKey);

    // attempt to locate searchKey in array a
    int subscript = linearSearch(a, searchKey, SIZE);

    // display results
    if (subscript != -1) {
        printf("Found value at subscript %d\n", subscript);
    }
    else {
        puts("Value not found");
    }
}

// compare key to every element of array until the location is found
// or until the end of array is reached; return subscript of element
// if key is found or -1 if key is not found
int linearSearch(const int array[], int key, size_t size) {
    // loop through array
    for (size_t n = 0; n < size; ++n) {
        if (array[n] == key) {
            return n; // return location of key
        }
    }

    return -1; // key not found
}
```

Enter integer search key: 36
Found value at subscript 18

```text
Enter integer search key: 37
Value not found
```

**Fig. 6.14** | Linear search of an array. (Part 2 of 2.)

### 6.10.2 Searching an Array with Binary Search
Linear searching works well for small or unsorted arrays. However, for large arrays, linear searching is inefficient. If the array is sorted, the high-speed binary search technique can be used.

The binary search algorithm eliminates from consideration *one-half* of a sorted array’s elements after each comparison. The algorithm locates the middle array element and compares it to the search key. If they’re equal, the algorithm found the search key, so it returns that element’s subscript. If they’re not equal, the problem is reduced to searching *one-half* of the array. If the search key is less than the middle array element, the algorithm searches the *first half* of the array; otherwise, it searches the *second half*. If the search key is not the middle element in the current subarray (a piece of the original array), the algorithm repeats on *one-quarter* of the original array. The search continues until the search key is equal to the middle element of a subarray, or until the subarray consists of one element that’s not equal to the search key—that is, the search key is not found.

### Performance of the Binary Search Algorithm
In the worst-case scenario, searching a sorted array of 1023 elements takes only 10 comparisons using a binary search. Repeatedly dividing 1,024 by 2 yields the values 512, 256, 128, 64, 32, 16, 8, 4, 2 and 1. The number 1,024 (2^10) is divided by 2 only 10 times to get the value 1. Dividing by 2 is equivalent to one comparison in the binary search algorithm. An array of 1,048,576 (2^20) elements takes a maximum of only 20 comparisons to find the search key. A sorted array of one billion elements takes a maximum of only 30 comparisons to find the search key. This is a tremendous increase in performance over a linear search of a sorted array, which requires comparing the search key to an average of half of the array elements. For a one-billion-element array, this is a difference between an average of 500 million comparisons and a maximum of 30 comparisons! The maximum comparisons for any array can be determined by finding the first power of 2 greater than the number of array elements.

### Implementing Binary Search
Figure 6.15 presents the iterative version of function binarySearch (lines 39–60). The function receives four arguments—an integer array b to search, an integer key to find, the low array subscript and the high array subscript. The last two arguments define the portion of the array to search. If the search key does not match the middle element of a subarray, the low subscript or high subscript is modified so that a smaller subarray can be searched:
