
## 7.2

Modify the above program such that a function is used to input values to the members and another function to display the time.

## 7.3

Design a function update that would accept the data structure designed in Exercise 7.1 and increments time by one second and returns the new time. (If the increment results in 60 seconds, then the second member is set to zero and the minute member is incremented by one. Then, if the result is 60 minutes, the minute member is set to zero and the hour member is incremented by one. Finally when the hour becomes 24, it is set to zero.)

## 7.4

Define a structure data type named date containing three integer members day, month and year. Develop an interactive modular program to perform the following tasks;

- To read data into structure members by a function
- To validate the date entered by another function
- To print the date in the format April 29, 2002 by a third function.

The input data should be three integers like 29, 4, and 2002 corresponding to day, month and year. Examples of invalid data: 31, 4, 2002 – April has only 30 days 29, 2, 2002 – 2002 is not a leap year

## 7.5

Design a function update that accepts the date structure designed in Exercise 7.4 to increment the date by one day and return the new date. The following rules are applicable:

- If the date is the last day in a month, month should be incremented
- If it is the last day in December, the year should be incremented
- There are 29 days in February of a leap year

## 7.6

Modify the input function used in Exercise 7.4 such that it reads a value that represents the date in the form of a long integer, like 19450815 for the date 15-8-1945 (August 15, 1945) and assigns suitable values to the members day, month and year. Use suitable algorithm to convert the long integer 19450815 into year, month and day.

## 7.7

Add a function called nextdate to the program designed in Exercise 7.4 to perform the following task;

- Accepts two arguments, one of the structure data containing the present date and the second an integer that represents the number of days to be added to the present date.
- Adds the days to the present date and returns the structure containing the next date correctly.

Note that the next date may be in the next month or even the next year.

## 7.8

Use the date structure defined in Exercise 7.4 to store two dates. Develop a function that will take these two dates as input and compares them;

- It returns 1, if the date1 is earlier than date2
- It returns 0, if date1 is later date

## 7.9

Define a structure to represent a vector (a series of integer values) and write a modular program to perform the following tasks:

- To create a vector
- To modify the value of a given element
- To multiply by a scalar value
- To display the vector in the form (10, 20, 30, . . . . . )

## 7.10

Add a function to the program of Exercise 7.9 that accepts two vectors as input parameters and return the addition of two vectors.

## 7.11

Create two structures named metric and British which store the values of distances. The metric structure stores the values in meters and centimeters and the British structure stores the values in feet and inches. Write a program that reads values for the structure variables and adds values contained in one variable of metric to the contents of another variable of British. The program should display the result in the format of

## 7.12

Define a structure named census with the following three members:

- A character array city [] to store names
- A long integer to store population of the city
- A float member to store the literacy level

Write a program to do the following:

- To read details for 5 cities randomly using an array variable
- To sort the list alphabetically
- To sort the list based on literacy level
- To sort the list based on population
- To display sorted lists

## 7.13

Define a structure that can describe a hotel. It should have members that include the name, address, grade, average room charge, and number of rooms.

Write functions to perform the following operations:

- To print out hotels of a given grade in order of charges
- To print out hotels with room charges less than a given value

## 7.14

Define a structure called cricket that will describe the following information:

player name
team name
batting average

Using cricket, declare an array player with 50 elements and write a program to read the information about all the 50 players and print a team-wise list containing names of players with their batting average.

## 7.15

Design a structure student_record to contain name, date of birth and total marks obtained.

Use the date structure designed in Exercise 7.4 to represent the date of birth.
Develop a program to read data for 10 students in a class and list them rank-wise.

## Key Terms

- Array: It is a collection of related data elements of same type.
- Structure: It is a collection of related data elements of different types.
- Dot operator: It is a member operator used to identify the individual members in a structure.
- Union: It is a collection of many members of different types.
- Bit field: It is a set of adjacent bits that holds data items and packs several data items in a word of memory.

## UNIT 8
File Handling

### 8.1 INTRODUCTION

Until now we have been using the functions such as scanf and printf to read and write data. These are console oriented I/O functions, which always use the terminal (keyboard and screen) as the target place. This works fine as long as the data is small. However, many real-life problems involve large volumes of data and in such situations, the console oriented I/O operations pose two major problems.

1. It becomes cumbersome and time consuming to handle large volumes of data through terminals.
2. The entire data is lost when either the program is terminated or the computer is turned off.

It is therefore necessary to have a more flexible approach where data can be stored on the disks and read whenever necessary, without destroying the data. This method employs the concept of files to store data. A file is a place on the disk where a group of related data is stored. Like most other languages, C supports a number of functions that have the ability to perform basic file operations, which include:

- naming a file,
- opening a file,
- reading data from a file,
- writing data to a file, and
- closing a file.

There are two distinct ways to perform file operations in C. The first one is known as the low-level I/O and uses UNIX system calls. The second method is referred to as the high-level I/O operation and uses functions in C's standard I/O library. We shall discuss in this chapter, the important file handling functions that are available in the C library. They are listed in Table 8.1.

### Table 8.1 High Level I/O Functions

| Function name | Operation |
|---|---|
| fopen() | * Creates a new file for use.<br>* Opens an existing file for use. |
| fclose() | * Closes a file which has been opened for use. |
| getc() | * Reads a character from a file. |
| putc() | * Writes a character to a file. |
| fprintf() | * Writes a set of data values to a file. |
| fscanf() | * Reads a set of data values from a file. |
| getw() | * Reads an integer from a file. |
| putw() | * Writes an integer to a file. |

| Function | Description |
|---|---|
| fseek() | * Sets the position to a desired point in the file. |
| ftell() | * Gives the current position in the file (in terms of bytes from the start). |
| rewind() | * Sets the position to the beginning of the file. |

There are many other functions. Not all of them are supported by all compilers. You should check your C library before using a particular I/O function.

### 8.2 TYPES OF FILES

As already explained, files are used for the storage and retrieval of data by a C program. Depending upon the format in which data is stored, files are primarily categorized into two types:

- **Text file:** As the name suggests, a text file stores textual information like alphabets, numbers, special symbols, etc. In actuality, the ASCII code of textual characters is stored in the text files. But, since data is stored in a storage device in the binary format, the text file contents are first converted in the binary form before actually being stored in the storage device. In other words, we can say that the text files store the ASCII encrypted information. A text file can store different character sets such as:
  - Upper case English alphabets (A to Z)
  - Lowercase English alphabets (a to z)
  - Numeric characters (like 1, 3, 5, etc.)
  - Punctuation characters (like :, ;, ', ?, etc.)
  - Special characters (like $, %, etc.)
  Some of the examples of text files include C source code files and files with .txt extension. C language supports various operations for manipulating data stored in a text file. Some of these operations include creating a new file, opening an existing file, reading a file, writing into the file, etc. These operations are performed with the help of inbuilt functions of C, explained later in the chapter.

- **Binary file:** As the name suggests, a binary file stores the information in the binary form, i.e., in the same format as it is stored in the memory. Thus, the use of binary file eliminates the need of data conversion from text to binary format for storage purpose. However, one of the main drawbacks of binary file is that the data stored in a binary file is not in human understandable form. Any file which stores the data in the form of bytes, i.e., 8-bit representation is known as binary file. Every executable file generated by the C compiler is a binary file. Apart from .exe files, examples of binary files include video stream files, image files, etc. C language supports binary file operations such as read, write and append with the help of various inbuilt functions.

### 8.3 DEFINING AND OPENING A FILE

If we want to store data in a file in the secondary memory, we must specify certain things about the file, to the operating system. They include:

1. Filename.
2. Data structure.
3. Purpose.

Filename is a string of characters that make up a valid filename for the operating system. It may contain two parts, a primary name and an optional period with the extension. Examples:
Input.data
store
