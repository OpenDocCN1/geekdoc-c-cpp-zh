# Checkpoint

10.15 Design an algorithm that uses a For loop to write the numbers 1 through 10 to a file.

10.16 What is the purpose of the eof function?

10.17 Is it acceptable for a program to attempt to read beyond the end of a file?

10.18 What would it mean if the expression eof(myFile) were to return True?

10.19 Which of the following loops would you use to read all of the items from the file associated with myFile?

+   a. While eof(myFile)
   Read myFile item
   End While
b. While NOT eof(myFile)
   Read myFile item
   End While

# 10.3 Using Files and Arrays

> **CONCEPT:** For some algorithms, files and arrays can be used together effectively. You can easily write a loop that saves the contents of an array to a file, and vice versa.

Some tasks may require you to save the contents of an array to a file so the data can be used at a later time. Likewise, some situations may require you to read the data from a file into an array. For example, suppose you have a file that contains a set of values that appear in random order and you want to sort the values. One technique for sorting the values in the file would be to read them into an array, perform a sorting algorithm on the array, and then write the values back to the file.

Saving the contents of an array to a file is a straightforward procedure: Open the file and use a loop to step through each element of the array, writing its contents to the file. For example, suppose a program declares an array as:

```
Constant Integer SIZE = 5
Declare Integer numbers[SIZE] = 10, 20, 30, 40, 50
```

The following pseudocode opens a file values.dat and writes the contents of each element of the numbers array to the file:

```
// Counter variable to use in the loop.
Declare Integer index
// Declare an output file.
Declare OutputStream numberFile
// Open the values.dat file.
Open numberFile "values.dat"
```