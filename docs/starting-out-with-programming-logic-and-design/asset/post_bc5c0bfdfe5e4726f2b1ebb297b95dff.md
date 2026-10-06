
# 344 Chapter 9 Sorting and Searching Arrays

Here is the pseudocode for the swap module:

```
Module swap(Integer Ref a, Integer Ref b)
// Local variable for temporary storage.
Declare Integer temp

// Swap the values in a and b.
Set temp = a
Set a = b
Set b = temp
End Module
```

Of course, this version of the swap module works only with Integer arguments. If we want to swap the contents of other types of variables, we would have to change the data type of the a and b parameters as well as the temp variable.

## Designing the Bubble Sort Algorithm

The bubble sort algorithm is usually incorporated into a program as a module. When you need to pass the array to the module and it sorts the array. Figure 9-10 shows a flowchart for a bubbleSort module that sorts an array of integers. Program 9-1 shows the pseudocode for the module. (Note that the pseudocode shown in Program 9-1 is only the bubbleSort module and not a complete program.)

Figure 9-10 Flowchart for the bubble sort algorithm

![](img/c939132f78787c7f339c6977b3fc8c85_368_0.png)

## Program 9-1 bubbleSort module
(not a complete program)

```
1 Module bubbleSort(Integer Ref array[], Integer arraySize)
2 // The element variable will contain the subscript
3 // of the last element in the array to compare.
4 Declare maxElement
5
6 // The index variable will be used as a counter
7 // in the inner loop.
8 Declare Integer index
9
10 // The outer loop positions maxElement at the last
11 // element to compare during each pass through the
12 // Initially, maxElement is the index of the
13 // last element in the array. During each iteration,
14 // it is decreased by one.
15 For maxElement = arraySize - 1 To 0 Step -1
16
17 // The inner loop steps through the array, comparing
18 // each element with its neighbor. All of the
19 // elements from 0 through maxElement are
20 // involved in the comparison. If two elements are
21 // out of order, they are swapped.
22 For index = 0 To maxElement - 1
23
24 // Compare an element with its neighbor and swap
25 // if necessary.
26 If array[index] > array[index + 1] Then
27 Call swap(array[index], array[index + 1])
28 End If
29 For
30 End For
31 End Module
```

In lines 4 and 8 the following variables are declared:

- The maxElement will hold the subscript of the last element that is to be compared to its immediate neighbor.
- The index variable is used as an array subscript of the loops.

The module uses two loops, nested inside another. The outer loop begins in line 15 as follows:

```
For maxElement = arraySize - 1 To 0 Step -1
```

This loop will iterate once for each element in the array's subscripts, it causes the maxElement variable to take on all of the array's subscripts, from the highest subscript down to 0. After each iteration, maxElement is decremented by one.

The second loop, which is nested inside the first loop, begins in line 22 as follows:

```
For index = 0 To maxElement - 1
```

## Chapter 9 Sorting and Searching Arrays

This loop iterates once for each of the unsorted array elements. It starts index at 0 and increments it up through maxElement - 1. During each iteration, the comparison in line 26 is prefixed:

```
If array[index] > array[index + 1] Then
```

This statement compares the element at array[index] with its neighbor array[index + 1]. If the element's neighbor is greater, the two are swapped in line 27. The swap module must also appear in any program that uses the module. The Following In Spotlight section shows how the bubble sort algorithm is used in a complete program.

![](img/c939132f78787c7f339c6977b3fc8c85_370_0.png)

## In the Spotlight:
Using the Bubble Sort Algorithm

Kathryn gets a grade of exams, she likes to see a list of the exam scores sorted from lowest to highest. She has asked you to design a program that will allow her to input a set of test scores and will display the scores sorted in ascending order. Here are the general steps in the algorithm:

1. Get the test scores from the user and store them in an array.
2. Sort the array in ascending order.
3. Display the contents of the array.

For testing purposes, you ask Kathryn whether you first design the program for her smallest class, which has only six students. If she is satisfied with the program, you can modify it to work with her other classes. She agrees with your plan.

Program 9-2 shows the pseudocode for the program, which is modularized. Rather presenting the entire program at once, we will first examine the main module, and then we will use the additional modules separately. Here is the main module:

## Program 9-2 Ascending score program: main module

| | |
| :--- | :--- |
| 1 | Module for the array size |
| 2 | // Constant the array size |
| 3 | Constant Integer SIZE = 6 |
| 4 | |
| 5 | |
| 6 | // Array to hold test scores |
| 7 | Declare Integer testScores[SIZE] |
| 8 | |
| 9 | // Get the test scores. |
| 10 | getScores(testScores, SIZE) |
| 11 | |
| 12 | // Sort the test scores. |
| 13 | bubbleSort(testScores, SIZE) |
| 14 | |
| 15 | // Display the test scores. |
| 16 | Display "Here are the test scores" |
| 17 | Display "sorted from lowest to highest." |
| 18 | showTestScores(testScores, SIZE) |
| 19 | |
| 20 | End Module |

## 9.1 The Bubble Sort Algorithm

Line 3 declares a constant, SIZE, that will be used as an array size declarator. The testScores array, which will hold the test scores, is declared. The testScores array, which will hold the test scores, is declared in line 6. In line 9 the testScores array and the SIZE constant are passed to the bubble module. As you will see in a moment, the testScores array is passed by reference. The purpose of this module is to get test scores from the user and store them in the array. Line 17 passes the testScores array and the SIZE constant to the showTestScores module. The module displays the values in the array. Next is the definition of the getTotalScores module, shown here:

## Program 9-2 Ascending score program (continued): getScores module

```
20 The getTotalScores module prompts the user
21 to enter scores into the array that is
22 passed as argument.
23 Module getTotalScores(Integer Ref array[], Integer arraySize)
24 // Counter variable
25 Declare Integer index
26
27 // Get the test scores.
28 For index = 0 to arraySize - 1
29 Display "Enter score number ", index + 1
30 Input array[index]
31 End For
32 End Module
```

The getTotalScores module has two parameters:

- array[]—An Integer is passed by reference to this parameter.
- arraySize—An Integer specifying the size of the array is passed into this parameter.

The purpose of this module is to display the contents of the array that is passed into the array parameter. The definitions of bubbleSort and swap modules appear next. These modules are the same presented earlier in this chapter.

## Program 9-2 Ascending score program (continued): bubbleSort and swap modules

```
34 The bubbleSort module accepts an array of Integers
35 and the array's size as arguments. When the module
36 is finished, the values in the array will be sorted
37 in ascending order.
38 Module bubbleSort(Integer Ref array[], Integer arraySize)
```

The showTestScores module appears next.

## Program 9-2 Ascending score program (continued): showTestScores module

```
82 The showTestScores displays the contents
83 of the array that is passed as argument.
84 Module showTestScores(Integer array[], Integer arraySize)
85 // Counter variable
86 Declare Integer index
87
88 // Display the test scores.
89 For index = 0 to arraySize - 1
90 Display array[index]
91 End For
92 End Module
```

## 9.1 The Bubble Sort Algorithm

Sorting an Array of Strings

Recall from Chapter 4 that most languages allow you to determine whether one string is greater than, equal to, or not equal to another string. As a result, you can design the bubble sort algorithm to work with an array of strings. This gives you the ability to sort an array of strings in alphabetical (ascending) order. The pseudocode in Program 9-3 shows an example. Notice that this program's versions of the bubbleSort and swap modules have been designed to work with String arrays.

# Program 9-3

```
1 Module main()
2 // Constant for the array size
3 Constant Integer SIZE = 6
```
