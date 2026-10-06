# Chapter 8

# Arrays

```
10 // Declare a counter variable for the loop.
11 Declare Integer index
12
13 // Calculate the total of the array elements.
14 For index = 0 To SIZE - 1
15 Set total = total + numbers[index]
16 End For
17
18 // Display the sum of the array elements.
19 Display "The sum of the array elements is ",
```

# Program Output

The sum of the array elements is 30

# Averaging the Values in an Array

The first step in calculating average of the values in an array is to get the total of the values. You saw how to do that with a loop in the preceding section. The second step is to divide the total by the number of elements in the array. The pseudocode 8-10 demonstrates the algorithm.

# Program 8-10

```
1 // Declare a constant for the array size.
2 Constant Integer SIZE = 5
3
4 // Declare an array initialized with values.
5 Declare Real scores[SIZE] = 2.5, 8.3, 6.5, 4.0, 5.2
6
7 // Declare and initialize an accumulator variable.
8 Declare Real total = 0
9
10 // Declare a variable to hold the average.
11 Declare Real average
12
13 // Declare a counter variable for the loop.
14 For index = 0 To SIZE - 1
15 Set total = total + numbers[index]
16 End For
17
18 // Calculate the average of the array elements.
19 Set average = total / SIZE
20
21 // Display the average of the array elements.
22 Display "The average of the array elements is ", average
```

# Program Output

The average of the array elements is 5.3