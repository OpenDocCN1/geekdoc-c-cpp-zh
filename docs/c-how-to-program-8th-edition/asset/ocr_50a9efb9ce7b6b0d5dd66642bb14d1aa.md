![](bbox=[0.243, 0.127, 0.824, 0.245])

**Fig. 8.19** | Graphical representation of the suit array.

The suit strings could be placed into a two-dimensional array, in which each row represents one suit and each column represents one of the letters of a suit name. Such a data structure must have a fixed number of columns per row, and that number must be as large as the largest string. Therefore, considerable memory is wasted when we store a large number of strings, of which most are shorter than the longest string. We use arrays of strings to help represent a deck of cards in the next section.

String arrays are commonly used with command-line arguments that are passed to function `main` when a program begins execution. Such arguments follow the program name when a program is executed from the command line. A typical use of command-line arguments is to pass options to a program. For example, from the command line on a Windows computer, the user can type

```
```text
dir /p
```
```

to list the contents of the current directory and pause after each screen of information. When the `dir` command executes, the option `/p` is passed to `dir` as a command-line argument. Such arguments are placed in a string array that main receives as an argument. We discuss command-line arguments in Appendix F, C Legacy Code Topics.

# 8.12 Function Pointers

A pointer to a function contains the function’s address in memory. We know that an array’s name is actually the address in memory of the first element. Similarly, a function’s name is actually the starting address in memory of the code that performs the function’s task. Pointers to functions can be passed to functions, returned from functions, stored in arrays, assigned to other function pointers and used to call the underlying function.

# *Multipurpose Selection Sort Using Function Pointers*

To illustrate the use of pointers to functions, Fig. 8.20 modifies the selection sort program of Fig. 8.13. Figure 8.20 consists of `main` (lines 13–50) and the functions `selectionSort` (lines 54–71), `swap` (lines 75–80), `ascending` (lines 84–87) and `descending` (lines 91–94). Function `selectionSort` receives a pointer to a function—either function `ascending` or function `descending`—as an argument in addition to the integer array to sort and the size of the array. Functions ascending and descending determine the sorting order. The program prompts the user to choose whether the array should be sorted in ascending order or in descending order (lines 20–22). If the user enters 1, a pointer to function ascending is passed to function `selectionSort` (line 33), causing the array to be sorted into increas-