# Program 8-2

```
1 // Declare an Integer array with 10 elements.
2 Declare Integer series[10]
3
4 // Declare a variable to use in the loop.
5 Declare Integer index
6
7 // Set each array element to 100.
8 For index = 0 To 9
9 Set series[index] = 100
10 End For
```

In line 2, an Integer array named series is declared, and in
line 5 an Integer variable named index is declared. The index variable is used as
counter in the For loop that appears in lines 8 through 10. In the loop, the index
variable takes on the values 0 through 9. The first time the loop iterates, index is set
to 0, so the statement in line 9 causes the array element series[0] to be set to 100.
The second time the loop iterates, index is set to 1, so the array series[1]
is set to 100. This continues until the last iteration, and by series[9] is set
to 100.

Let’s look at another example. Program 8-1 could be simplified by using For
loops: for inputting values into the array and for displaying the con-
tents of the array. This is shown in Program 8-3.

![](bbox=[0.313, 0.545, 0.363, 0.574])

# Program 8-3

```
1 // Create a constant for the size of the array.
2 Constant Integer SIZE = 3
3
4 // Declare an array to hold the number of hours
5 // worked by each employee.
6 Declare Integer hours[SIZE]
7
8 // Declare a variable to use in the loops.
9 Declare Integer index
10
11 // Get the hours for each employee.
12 For index = 0 To SIZE - 1
13 Display "Enter the hours worked by"
14 Display "employee number ", index + 1
15 Input hours[index]
16 End For
17
18 // Display the values entered.
19 Display "The hours you entered:"
20 For index = 0 To SIZE - 1
21 Display hours[index]
22 End For
```