
values entered by the user, and line 15 declares an Integer variable named index that will be used in a loop to step through the array, displaying its elements.

Line 19 prompts the user to enter a number or -1 to quit. This program uses the value -1 as a sentinel value. When the user enters -1, the program will stop reading input. Line 20 reads the user's input and stores it in the number variable. A while loop begins in line 24. The loop iterates as long as number not -1 and count is less than size. Inside the loop, in line 26 the numbers variable is assigned to values[count], and in line 29 the count variable is incremented. Each time a number is assigned to an array element, the count variable is incremented. As a result, the count variable will hold the number of elements that are stored in the array. Then, line 32 prompts the user to enter another number (or -1 to quit) and line 33 reads the user's input into the number variable. The loop then starts. When the user enters -1, or count reaches the size of the array, the For loop begins in line 38 displays all of the elements that are stored in the array. Rather than stepping through all of the elements in the array, however, the loop steps through only elements that contain values. Notice that the index variable's starting value is 0, and its ending value is count-1. By setting the value to count-1 rather than size, the loop will stop when the element containing the last value has been displayed, not when the end of the array has been reached.

## Optional Topic: The For Each Loop

Several languages provide a specialized version of the For loop known as For Each loop. The For Each loop can simplify array processing when your task is to step through an array, retrieving the value of each element. The For Each loop is typically used in the following general format:

```For var In array
    statement
    statement
    etc.
End For
```

In the general format, var is the name of a variable and array is the name of an array. The loop will iterate for every element in the array. Each time the loop iterates, it copies an array element to the var variable. For example, the first time the loop iterates, var will contain the value of array[0], the second time the loop iterates var will contain the value of array[1], and so forth until the loop has stepped through all elements in the array. For example, suppose we have the following declarations:

```Constant Integer SIZE = 5
Declare Integer numbers[SIZE] = 5, 10, 15, 20, 25
Declare Integer num
```

The following For Each loop can be used to display all the values stored in the numbers array:

```For Each num In numbers
    Display num
End For
```

## 8.2 Sequentially Searching an Array

NOTE: The For Each loop is not available in all languages, so we will continue to use the regular For loop in our examples.

### Checkpoint

- 8.1 Can you store a mixture of data types in an array?
- 8.2 What is array size?
- 8.3 In most languages, can the size of an array be changed while the program is running?
- 8.4 What is an array element?
- 8.5 What is a subscript?
- 8.6 What is usually the first subscript in an array?
- 8.7 Look at the following pseudocode: `Integer SIZE = 7 Declare Real numbers[SIZE]` and answer questions:
    - a. What is the name of the array that is declared?
    - b. What is the size of the array?
    - c. What data type are the array elements?
    - d. What is the subscript of the last element in the array?
- 8.8 What does “array bounds checking” mean?
- 8.9 What is an off-by-one error?

## Sequentially Searching an Array

CONCEPT: The sequential search algorithm is a simple technique for finding an item in an array. It steps through the array, beginning at the first element and compares each element to the item being searched. The search stops when the item is found or the end of the array is reached.

Programs need to search for data that is stored in an array. Various techniques known as search algorithms have been developed to locate a specific item in a larger collection of data, such as an array. This section shows how to use the simplest of all algorithms—the sequential search. The sequential search uses a loop to sequentially step through an array, starting with the first element. It compares each element with the value being searched for and stops when the value is found or the end of the array is reached. If the value is not in the array, the algorithm unsuccessfully searches to the end of the array.

Figure 8-5 shows the general logic of the sequential search algorithm. Here is a summary of the data items in the figure:

- array is the array being searched.
- searchValue is the value that the algorithm is searching for.
- found is a Boolean variable that is used as a flag. Setting found to False indicates that searchValue has not been found. Setting found to True indicates that searchValue has been found.
- index is an Integer variable used as a loop counter.

When the algorithm finishes, the found variable will be set to True if the searchValue was found in the array. When this is the case, the index variable will be set to the subscript of the element containing the searchValue.![](img/c939132f78787c7f339c6977b3fc8c85_322_0.png)

If the searchValue was not found in the array, found will be set to False. The following shows how you can express this logic in pseudocode:

```
Set found = False
Set index = 0
While found = False AND index <= SIZE - 1
  If array[index] == searchValue Then
    Set found = True
  Else
    Set index = index + 1
  End If
End While
```

The pseudocode in Program 8-6 demonstrates how to implement the sequential search in a program. This program has an array that holds test scores. It sequentially searches the array for a score of 100. If a score of 100 is found, the program displays the number.

# Program 8-6

```Constant for the array size.
Constant Integer SIZE = 10

// Declare an array to hold test scores.
Declare Integer scores[SIZE] = 87, 75, 98, 100, 82, 72, 88, 60, 78

// Declare a Boolean variable to act as a flag.
Declare Boolean found

// Declare a variable to use as a loop counter.
Declare Integer index

// The flag must initially be set to False.
Set found = False

// Set the counter variable to 0.
Set index = 0

// Step through the array searching for
// score equal to 100.
While found == False AND index <= SIZE - 1
  If scores[index] == 100 Then
    Set found = True
  Else
    Set index = index + 1
  End If
End While

// Display the search results.
If found Then
  Display "You earned 100 on test number ", index + 1
Else
  Display "You did not earn 100 on any test."
End If
```

Program Output
nYou earned 100 on test number 4

## Searching a String Array

Program 8-6 demonstrates how to use the sequential search to find a specific number in an Integer array. As shown in Program 8-7, you can also use the algorithm to find a string in a String array.

# Program 8-7

```
Declare a constant for the array size.
Constant Integer SIZE = 6

// Declare a String array initialized with values.
Declare String names[SIZE] = "Ava Fischer", "Chris Rich",
                    "Gordon Pike", "Matt Hoyle",
                    "Rose Harrison", "Giovanni Ricci"

// Declare a variable to hold the search value.
Declare String searchValue

// Declare a Boolean variable to act as a flag.
Declare Boolean found

// Declare a counter variable for the array.
Declare Integer index

// The flag must initially be set to False.
Set found = False

// Set the counter variable to 0.
Set index = 0

// Get the string to search for.
Display "Enter a name to search for in the array."
Input searchValue

// Step through the array searching for
// the specified name.
While found == False AND index <= SIZE - 1
  If names[index] == searchValue Then
    Set found = True
  Else
    Set index = index + 1
  End If
End While

// Display the search results.
If found Then
  Display "The name was found at position ", index + 1
Else
  Display "The name was not found in the array."
End If
```
