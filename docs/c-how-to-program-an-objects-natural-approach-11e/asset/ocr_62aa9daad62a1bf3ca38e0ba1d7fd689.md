```
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
```

**Fig. 2.1.2** | Binary search of an array. (Part 3 of 3.)

# Function Template binarySearch

Lines 26–59 define the `binarySearch` function template. Its function parameters are:

+   - a reference to the array to search, and
+   - a reference to the search key

Lines 28–30 calculate the low-end index, high-end index and middle index of the portion of the array that the algorithm is currently searching. When binarySearch is first called, low is 0, high is the array’s size minus 1, and middle is the average of these two values. Line 31 initializes location to −1—the value binarySearch returns if the search key is not found. Lines 33–56 loop until

+   - low is greater than high, indicating that the element was not found, or
+   - location does not equal -1, indicating that the search key was found.

Line 45 tests whether the value in the middle element is equal to key. If so, line 46 assigns the middle index to location, the loop terminates, and the function returns location to