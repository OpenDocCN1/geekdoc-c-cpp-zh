# 8.1 Array Basics

```
8 // that are actually stored in the array.
9 Declare Integer count = 0
10
11 // Declare an Integer variable to hold the user's input.
12 Declare Integer number
13
14 // Declare a variable to step through the array.
15 Declare Integer index
16
17 // Prompt the user to enter a number. If the user enters the
18 sentinel value -1 we will stop accepting input.
19 Display "Enter a number or -1 to quit"
20 Input number
21
22 // If the input is not -1 and the array is not
23 // full, process the input.
24 While (number != -1 AND count < SIZE)
25 // Store the input in the array.
26 Set values[count] = number
27
28
29 // Increment count.
30 count = count + 1
31
32 // Prompt the user for the next number.
33 Display "Enter a number or -1 to quit"
34 Input number
35 End While
36
37 // Display the values stored in the array.
38 Display "Here are the numbers you entered:"
39 For index = 0 To count - 1
40 Display values[index]
41 End For
```

# Program Output (with Input Shown in Bold)

```
Enter a number or -1 to quit.
**2 [Enter]**
Enter a number or -1 to quit.
**4 [Enter]**
Enter a number or -1 to quit.
**6 [Enter]**
Enter a number or -1 to quit.
**1 [Enter]**
Here are the numbers you entered:
```

Let's examine the pseudocode in detail. Line 2 declares a constant, SIZE, initialized with the value 100. Line 5 declares an Integer array named values, using SIZE as the size declara-ntor. As a result, the values array will have 100 elements. Line 9 declares an Integer variable named count, which will hold the number of items that are stored in the array. Notice that count is initialized with 0 because there are no values stored in the array. Line 12 declares an Integer variable named number that will hold