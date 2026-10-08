
## 18.2 Searching Algorithms

### Implementing Binary Search
Figure 18.3 declares class BinarySearchTest, which contains static methods Main, BinarySearch and DisplayElements (which helps visualize the binary search algorithm). Method Main has local variables a Random object generator (line 10) to produce random int values and the int array data (line 11) to store randomly ints. Lines 14-17 generate ints in the range 10-99 and store them in data. Recall that a binary search requires an array's elements to be sorted. For this, line 19 calls Array's static method Sort for the data array—this sorts the elements in ascending order. Line 20 outputs the array's contents by calling DisplayElements (lines 86-98). Lines 23-24 prompt the user for the search key and store it in searchInt. Line 30 calls BinarySearch to determine whether searchInt is in the array. If BinarySearch returns the element's index, which is displayed in lines 33-35. If searchInt is not in the array, BinarySearch returns -1, and lines 39–45 prompt for and retrieve the integer from the user.

```cs
// Fig. 18.3: BinarySearchTest.cs
// Class that contains an array of random integers and a method
// that uses binary search to find an integer.
using System;
public class BinarySearchTest {
    static void Main() {
        var generator = new Random();
        int[] data = new int[15]; // create space for array

        // fill array with random ints in range 10-99
        for (var i = 0; i < data.Length; i++) {
            data[i] = generator.Next(10, 100);
        }

        Array.Sort(data); // elements must be sorted in ascending order
        DisplayElements(data, 0, data.Length - 1); // display array
        Console.Write("enter an integer value (-1 to quit):");
        int searchInt = int.Parse(Console.ReadLine());

        // repeatedly prompt an input: -1 terminates the app
        while (searchInt != -1) {
            // perform binary search
            int position = BinarySearch(data, searchInt);
            if (position != -1) // integer was found
        }
    }
}
```

> Fig. 18.3 | Class that contains an array of random integers and a method that uses binary search to find an integer. (Part I of 3).

## Chapter 18 Searching and Sorting

```cs
            Console.WriteLine("The integer ${searchInt} was found in " +
                "${position}[position].\n\n");
        } else // integer was not found
        {
            Console.WriteLine("The integer was not found.\n");
        }
        // input next from user
        Console.Write("Please enter an integer value (-1 to quit: ");
        searchInt = int.Parse(Console.ReadLine());
    }
    // perform a binary search on the data
    public static int BinarySearch(int[] values, int searchElement)
    {
        var low = 0; // low end of the search area
        var high = values.Length - 1; // high end of the search area
        var middle = (low + high + 1) / 2; // middle element
        do // loop to search for element
            // displaying remaining elements of array
            DisplayElements(values, low, high);
            // indicate current middle; pad left with spaces for alignment
            Console.WriteLine("--".PadLeft((middle + 1) * 3));
            // if the element is found at the middle
            if (searchElement == values[middle])
                return middle; // search key found, return its index
            // middle element is too high
            else if (searchElement < values[middle])
            {
                high = middle - 1; // eliminate the higher half
            }
            else // middle element is too low
            {
                low = middle + 1; // eliminate the lower half
            }
            middle = (low + high + 1) / 2; // recalculate the middle
        } while (low <= high);
        return -1; // search key was not found
    }
```

![](img/57baed2319be0bb1b5f98674846f2711_790_0.png)

## 18.2 Searching Algorithms

```cs
85 // method to output certain values in array
86 public static void DisplayElements(int[] values, int low, int high)
87 {
88 // output three spaces for each element up to low for alignment
89 Console.Write(string.Empty.PadLeft(low * 3));
90
91 // output elements left in array
92 for (var i = low; i <= high; ++i)
93 {
94 Console.Write($"{values[i]}");
95 }
96
97 Console.WriteLine();
98
99 }
```

| 12 | 17 | 22 | 25 | 30 | 39 | 40 | 52 | 56 | 72 | 76 | 82 | 84 | 91 | 93 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Please enter an integer value (-1 to quit): 72 | | | | | | | | | | | | | |
| 12 | 17 | 22 | 25 | 30 | 39 | 40 | 52 | 56 | 72 | 82 | 84 | 91 | 93 |
| | | | | | | | | 56 | 72 | 76 | 82 | 84 | 91 | 93 |
| | | | | | | | | 56 | 76 | | | | | |
| The integer 72 was found in position 9. | | | | | | | | | | | | | | |
| Please enter an integer value (-1 to quit): 13 | | | | | | | | | | | | | | |
| 12 | 17 | 22 | 25 | 30 | 39 | 40 | 52 | 56 | 72 | 82 | 84 | 91 | 93 |
| | 12 | 17 | 22 | 25 | 30 | 39 | 40 | | | | | | | |
| | | 12 | 17 | 22 | | | | | | | | | |
| | | | 12 | | | | | | | | | | |
| The integer 13 was not found. | | | | | | | | | | | | | | |
| Please enter an integer value (-1 to quit): -1 | | | | | | | | | | | | | | |

> Fig. 18.3 | Class that contains an array of random integers and a method that uses binary search to find an integer. (Part 3 of 3.)

The first line of output from this app is the array of ints, in increasing order. When the user inputs the app to search for 72, the app tests the middle element (indicated by -- below the element in the output), which is 52. The search key is greater than 52, so the app eliminates from consideration the first half of the array and the middle element from the second half. The search key is smaller than 82, so the app eliminates the second half of the subarray, leaving only three elements. Finally, the app checks 72 (which matches the search key) and returns the index 9. PadLeft (lines 62 and 89) adds the specified number of spaces to the beginning of the string on which the method is called and returns a new string containing the results.

## Chapter 18 Searching Sorting

### Method BinarySearch

Lines 50–83 declare method BinarySearch, which receives as parameters the array to search and the search key. Lines 52–54 calculate the *low end index*, high end index and *middle* of the array being searched. When the method is first called, the *low* index is 0, the high index is the length of the array minus 1 Lines 56–80 loop until *low* is greater than *high* (this occurs when the element is not found). Lines 65 tests whether the value is equal to search. If this is true, 67 returns *middle*—the search key's location—to the caller. Each iteration of the loop (lines 59 and 72) eliminates half of the array then adjusts the *middle* for the next iteration.

### Efficiency of Binary Search
In the worst-case scenario, searching a sorted array of 1,023 elements causes BinarySearch to iterate only 10 times. Dividing 1023 by 2 (because we remove the middle element) and rounding down yields 511, 255, 127, 63, 31, 15, 7, 3, 1 and 0. Dividing by 2 is equivalent to one loop iteration in the binary search. Thus, an array of 1,048,575 ($2^{20} - 1$) elements takes a maximum of 20 to 30 iterations. This is a tremendous improvement over the linear search. For a billion-element array, this is a difference between an average of 500 iterations for the linear search and 30 iterations for the binary search! The number of iterations needed for the binary search of any sorted array is the exponent of the power of 2 that the number of elements in the array, which is represented as $\log n$. All logarithms grow at roughly the same rate, in Big O notation the base is omitted. This results in a Big O of $O(\log n)$ for a binary search, which is also known as logarithmic runtime.

## 18.3 Sorting Algorithms
Sorting data (i.e., placing the data in some particular order, such as *ascending or descending*) is one of the most important computing applications. A bank sorts by check account number so that it can prepare individual bank statements at the end of each month. Telephone companies sort their lists of accounts by name and last, and by first name to make it easy to find phone numbers. Virtually every organization will sort some data— has attracted substantial, compute-intensive problem research.

It's important to understand that sorting is the *end result*—the sorted array. The choice of algorithm affects only the runtime and *memory use* of the app. The rest of the chapter introduces three common sorting algorithms. The first two—*selection sort* and *insertion sort*—are simple to program, but inefficient. The last—*merge sort*—is much faster than selection sort and insertion sort but more difficult to program. We focus on sorting arrays of simple-
