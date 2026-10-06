Write a pseudocode algorithm that uses the For Each loop to display all the values in the following array:

Constant Integer SIZE = 10
Declare Integer values[SIZE] = 1, 2, 3, 4, 5, 6, 7, 8, 9, 10

# Debugging Exercises

+   1. What is the error in the following pseudocode?

```
// This program uses an array to display five names.
Constant Integer SIZE = 5
Declare String names[SIZE] = "Meg", "Jack", "Steve", "Bill", "Lisa"
Declare Integer index
For index = 0 To SIZE
  Display names[index]
End For
```

+   2. What is the error in the following pseudocode?

```
// This program displays the highest value in the array.
Constant Integer SIZE = 3
Declare Integer values[SIZE] = 1, 3, 4
Declare Integer index
Declare Integer highest
For index = 0 To SIZE - 1
  If values[index] > highest
    Set highest = values[index]
End If
```

Display "The highest number is ", highest

+   3. What is the error in the following pseudocode?

// The searchName function accepts a string containing the name
// to search, an array of strings and an integer specifying the size of the array. The function
// searches for the name in the array. If the name is found, the string containing the name is returned; otherwise a message
 indicating that the name was not found in the array is
 returned.

```
Function searchName(String name, String names[],
  Declare Boolean found
  Declare Integer index
  Declare String result
  // Step through the array searching for the
  // specified name.
  While found == False AND index <= size - 1
    If contains(names[index], name) Then
      Set found = True
    Else
      Set index = index + 1
    End If
End While
```