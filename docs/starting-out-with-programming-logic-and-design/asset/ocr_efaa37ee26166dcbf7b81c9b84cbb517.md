# In the Spotlight:

# Using the Binary Search Algorithm

Constance manages a cooking school that employs six instructors. She has asked you to design a program that she can use to look up an instructor's phone number. You decide to use two parallel arrays: one names that will hold the instructors' names, and another names that will hold each instructor's phone number. Here is the general algorithm:

+   1. Get an instructor's last name from the user.
2. Search for the name in the names array.
3. If the name is found, get its subscript. Use the subscript to display the contents of the parallel arrays array. If the name is not found, display a message indicating...

Program 9-8 shows the pseudocode for the program. Note that the array contents are already sorted in ascending order. This is important because the program uses the binary search algorithm to locate a name in the names array.

# Program 9-8

```
Module main()
  // Constant for array sizes
  Integer SIZE = 6

// Array of instructor names, already sorted in
// ascending order.
Declare String names[SIZE] = "Hall", "Harrison"
  "Hoyle", "Kimura"
  "Lopez", "Pike"

// Parallel array of instructor phone numbers.
Declare String phones[SIZE] = "555-6783", "555-0199"
  "555-9974", "555-2377"
  "555-7772", "555-1716"

// Variable to hold the last name to search for.
Declare String searchName

// Variable to hold the subscript of the name.
Declare Integer index

// Variable to control the loop.
Declare String again = "Y"
While (again == "Y" OR again == "y")n  // Get the name to search for.
  Display "Enter a name to search for"
  Input searchName

  // Search for the last name.
  index = binarySearch(names, searchName, SIZE)
```