# Chapter 8 Arrays

```
33 Else
34    Display "You did not earn 100 on any test."
35    End If
```

Program Output
nYou earned 100 on test number 4

# Searching a String Array

Program 8-6 demonstrates how to use the sequential search algorithm to find a specific number in an Integer array. As shown in Program 8-7, you can also use the algorithm to find a string in a String array.

# Program 8-7

```
1 // Declare a constant for the array size.
2 Constant Integer SIZE = 6
3
4 // Declare a String array initialized with values.
5 Declare String names[SIZE] = "Ava Fischer", "Chris Rich"
6                    "Gordon Pike", "Matt Hoyle"
7                    "Rose Harrison", "Giovanni Ricci"
8
9 // Declare a variable to hold the search value.
10 Declare String searchValue
11
12\13 // Declare a Boolean variable to act as a flag.
14 Declare Boolean found
15
16 // Declare a counter variable for the array.
17 Declare Integer index
18
19 // The flag must initially be set to False.
20 Set found = False
21
22 // Set the counter variable to 0.
23 Set index = 0
24
25 // Get the string to search for.
26 Display "Enter a name to search for in the array."
27 Input searchValue
28
29 // Step through the array searching for
30 // the specified name.
31 While found == False AND index <= SIZE - 1
32    If names[index] == searchValue Then
33        Set found = True
34    Else
35        Set index = index + 1
36    End If
37 End While
```

![](bbox=[0.305, 0.327, 0.347, 0.363])