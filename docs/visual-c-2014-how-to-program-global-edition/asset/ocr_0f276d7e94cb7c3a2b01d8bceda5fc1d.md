# 18.3 Sorting Algorithms 793

type data, namely, ints. It's possible to sort arrays of objects as well—we discuss this in Chapter 21, Generic Collections; Functional Programming with LINQ/PLINQ.

# Sorting Visualizations

In the text, we add output statements to help you visualize how each sort works. The web is loaded with visual animations that show these sorts in action. Simply search for the algorithm name and “animation.”

# 18.3.1 Selection Sort

Selection sort is a simple, but inefficient, algorithm. The first iteration of the algorithm selects the smallest element in the array and swaps it with the first element. The second iteration selects the smallest element (which is the smallest remaining element) and swaps it with the second element. The algorithm continues until the last iteration selects the largest element and, if necessary, swaps it with the second-to-last element, leaving the largest element in the last position. After the iteration, i elements of the array will be sorted in increasing order in the first i positions of the array.

For the following discussion, we highlight the smallest element in bold and italic, and the element with which it will be swapped in bold. Consider the array

| 34 | 56 | 4 | 10 | 77 | 51 | 93 | 30 | 5 | 52 |

A sort begins from index 0 and determines the smallest element (4). The app then swaps 4 with the element at index 0 (3), resulting in

| 4 | 56 | 34 | 10 | 77 | 51 | 93 | 30 | 5 | 52 |

The second iteration begins from index 1 and determines the smallest value of the remaining elements (5). The app then swaps 5 with the element at index 1 (6), resulting in

| 4 | 5 | 34 | 10 | 77 | 51 | 93 | 30 | 56 | 52 |

The third iteration begins from index 2 and determines the next smallest value (10). The app then swaps 10 with the element at index 2 (3), resulting in

| 4 | 5 | 10 | 34 | 77 | 51 | 93 | 30 | 56 | 52 |

The process continues until the array is fully sorted:

| 4 | 5 | 10 | 30 | 34 | 51 | 52 | 56 | 77 | 93 |

After the first iteration, the smallest element is in the first position. After the second iteration, the two smallest elements are in order in the first two positions. After the third iteration, the three smallest elements are in order in the first three positions.

# Implementing Selection Sort

In Fig.84, Main declares local variables a Random object named generator to produce random int's and the int array (line 11) to store randomly generated ints. Lines 14–17 generate random ints in range 10–99 and store them in data. Line 20 outputs the array's unsorted contents. Line 22 calls selectionSort to sort array's contents in ascending order. Lines 24–25 show the sorted array. Method SelectionSort calls PrintArray (defined in lines 59–86) to help visualize the sorting algorithm. The output uses dashes to indicate the position of the array that is sorted after each pass of the algorithm. An asterisk is placed next to the position of the element that