
```cpp
54        middle = (low + high + 1) / 2; // recalculate the middle
55    } while ((low <= high) && (location == -1));
56
57    return location; // return location of key
58
59 }
60
61 int main() {
62    // use the default random-number generation engine to produce
63    // uniformly distributed pseudorandom int values from 10 to 99
64    std::random_device rd; // used to seed the default_random_engine
65    std::default_random_engine engine{rd()}; // rd() produces a seed
66    std::uniform_int_distribution<int> randomInt{10, 99};
67
68    std::array<int, 15> arrayToSearch; // create 15-element array
69
70    // fill arrayToSearch with random values
71    for (int& item : arrayToSearch) {
72        item = randomInt(engine);
73    }
74
75    std::sort(arrayToSearch.begin(), arrayToSearch.end());
76
77    // display arrayToSearch's values
78    displayElements(arrayToSearch, 0, arrayToSearch.size() - 1);
79
80    // get input from user
81    std::cout << "\nPlease enter an integer value (-1 to quit): ";
82    int searchKey; // value to locate
83    std::cin >> searchKey; // read an int from user
84    std::cout << "\n";
85
86    // repeatedly input an integer; -1 terminates the program
87    while (searchKey != -1) {
88        // use binary search to try to find integer
89        int position{binarySearch(arrayToSearch, searchKey)};
90
91        // return value of -1 indicates integer was not found
92        if (position == -1) {
93            std::cout << std::format("{} was not found.\n", searchKey);
94        }
95        else {
96            std::cout << std::format("{} was found in position {}.\n",
97                searchKey, position);
98        }
99
100        // get input from user
101        std::cout << "\n\nPlease enter an integer value (-1 to quit): ";
102        std::cin >> searchKey; // read an int from user
103        std::cout << "\n";
104    }
105 }
```

**Fig. 21.2** | Binary search of an array. (Part 2 of 3.)

```text
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97

Please enter an integer value (-1 to quit): 48
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                         *
10 23 27 48 52 55 58
             *
48 was found in position 3.

Please enter an integer value (-1 to quit): 92

10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                         *
                         62 63 68 72 75 92 97
                                             *
                                             75 92 97
                                                *
92 was found in position 13.

Please enter an integer value (-1 to quit): 22
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                         *
10 23 27 48 52 55 58
             *
10 23 27
   *
10
*
22 was not found.

Please enter an integer value (-1 to quit): -1
```

**Fig. 21.2** | Binary search of an array. (Part 3 of 3.)

## Function Template binarySearch

Lines 26–59 define the `binarySearch` function template. Its function parameters are:

- a reference to the array to search, and
- a reference to the search key

Lines 28–30 calculate the low-end index, high-end index and middle index of the portion of the array that the algorithm is currently searching. When binarySearch is first called, low is 0, high is the array’s size minus 1, and middle is the average of these two values. Line 31 initializes location to −1—the value binarySearch returns if the search key is not found. Lines 33–56 loop until

- low is greater than high, indicating that the element was not found, or
- location does not equal -1, indicating that the search key was found.

Line 45 tests whether the value in the middle element is equal to key. If so, line 46 assigns the middle index to location, the loop terminates, and the function returns location to the caller. Each loop iteration that does not find the search key tests a single value (line 48) and eliminates half of the remaining values in the array (line 49 or 51).

## Function main

Lines 64–66 set up a random-number generator for int values from 10–99. Lines 68–73 create an array and fill it with random ints. Recall that the binary search algorithm requires a sorted array, so line 75 uses `std::sort` to sort arrayToSearch’s elements into ascending order. Then, line 78 displays arrayToSearch’s sorted contents.

Lines 87–104 loop until the user enters the value −1. For each search key the user enters, the program performs a binary search of arrayToSearch to determine whether it contains that search key. First, we show arrayToSearch’s contents in ascending order. When the user instructs the program to search for 48, binarySearch tests the middle element—60, as indicated by *. The search key is less than 60, so the program eliminates the array’s second half and tests the middle element from the array’s first half. The search key equals 48, so the program returns the index 3 after performing just two comparisons. The output also shows the results of searching for the values 92 and 22.

## 21.4.2 Efficiency of Binary Search

In the worst-case scenario, searching a sorted array of 1,023 elements (2¹⁰ − 1) takes only **10 comparisons** with binary search. The algorithm compares the search key to the middle element of the sorted array. If it’s a match, the search is over. Otherwise, if the search key is larger than the middle element, we can eliminate the array’s first half from further consideration, and if it’s smaller, we can eliminate the array’s second half from further consideration. This creates a halving effect—subsequent searches have to search only 511, 255, 127, 63, 31, 15, 7, 3 and 1 elements. The number 1,023 (2¹⁰ − 1) needs to be halved only 10 times to either find the key or determine that it’s not in the array.

Dividing by 2 is equivalent to one comparison in the binary search algorithm. Thus, an array of 1,048,575 (2²⁰ − 1) elements takes a **maximum of 20 comparisons** to find the key, and an array of about one billion elements takes a **maximum of 30 comparisons** to find the key—tremendous performance improvements over the linear search. For a one-billion-element array, this is the difference between an average of 500 million comparisons for the linear search and a maximum of only 30 comparisons for the binary search!

The maximum number of comparisons needed for the binary search of any sorted array is the exponent of the first power of 2 greater than the number of elements in the array, which is represented as log₂ n. All logarithms grow at “roughly the same rate,” so the base can be omitted for Big O purposes. This results in a Big O of O(log n) for a binary search, known as logarithmic running time and pronounced as “order log n.”

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1265_0.png)

## Checkpoint

1. *(Fill-in)* The linear search and the binary search are dramatically different search algorithms. Yet, for each, the worst-case runtime occurs when ________.
   **Answer:** the search key is not found.

2. *(Discussion)* It’s expensive to sort an array to enable it to be searched efficiently with the binary search algorithm. Mention two circumstances making it worthwhile to do this.
   **Answer:** 1. When the array will be searched a great many times. 2. When the application has strict performance requirements.

3. *(Discussion)* Compare the worst-case performance of a linear search on an unsorted trillion-element array with the worst-case performance of a binary search on a trillion-element sorted array.
   **Answer:** The linear search would have to perform about a trillion comparisons to determine that the search key doesn’t match an item in the unsorted array or matches an element close to the array’s end. The binary search would have to perform about 40 comparisons to determine that the search key either doesn’t match an item in the sorted array or matches an item on the last few comparisons.

## 21.5 Insertion Sort

Next, let’s implement a sorting algorithm. The insertion sort algorithm’s first iteration takes the array’s second element and, if it’s less than the first element, swaps it with the first element—that is, the algorithm inserts the second element in front of the first element. The second iteration looks at the third element and inserts it into the correct position with respect to the first two elements so all three elements are in order.

### First Iteration

Line 27 of Fig. 21.3 declares and initializes the array named `data` with the following values:

```text
34   56   4   10   77   51   93   30   5   52
```

Line 36 passes the array to the `insertionSort` function, which receives the array in parameter `items`. The function first looks at items[0] and items[1], whose values are 34 and 56, respectively. These two elements are already in order, so the algorithm continues. If they were out of order, the algorithm would swap them.

### Second Iteration

In the second iteration, the algorithm looks at the value of items[2] (that is, 4). This value is less than 56, so the algorithm stores 4 in a temporary variable and moves 56 one element to the right. The algorithm then determines that 4 is less than 34, so it moves 34 one element to the right. At this point, the algorithm has reached the beginning of the array, so it places 4 in items[0]. The array is now:

```text
4   34   56   10   77   51   93   30   5   52
```

### Third Iteration and Beyond

In the third iteration, the algorithm places the value of items[3] (that is, 10) in the correct location with respect to the first four array elements. The algorithm compares 10 to 56 and moves 56 one element to the right because it’s larger than 10. Next, the algorithm compares 10 to 34, moving 34 one element to the right. When the algorithm compares 10 to 4, it observes that 10 is greater than 4 and places 10 in items[1]. The array is now:

```text
4   10   34   56   77   51   93   30   5   52
```

With this algorithm, after the *i*th iteration, the first *i* + 1 array elements are sorted. However, they may not be in their final locations because the algorithm might encounter smaller values later in the array.
