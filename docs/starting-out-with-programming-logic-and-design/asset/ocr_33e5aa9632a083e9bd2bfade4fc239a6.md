# 8 Arrays

# TOPICS

| 8.1 Array Basics | 8.4 Parallel Arrays |
| 8.2 Sequentially Searching an Array | 8.5 Two-Dimensional Arrays |
| 8.3 Processing the Contents of an Array | 8.6 Arrays of Three or More Dimensions |

# 8.1 Array Basics

> **CONCEPT:** An array allows you to store a group of items of the same data type together in memory. Processing a large number of items in an array is usually easier than processing a large number of items stored in separate variables.

In the programs you have designed so far, you have used variables to store data in memory. In most programming languages, the simplest way to store a value in memory is to store in a variable. Variables work well in many situations, but they have limitations. For example, they can only hold one value at a time. Consider the following pseudocode declaration:

```
Declare Integer number = 99
```

This pseudocode statement declares an Integer variable named number, initialized with the value 99. Consider what happens if the following statement appears later in the program:

```
Set number = 5
```

This statement assigns the value 5 to number, replacing the value 99 that was previously stored. Because number is an ordinary variable, it can hold only one value at a time.

Because variables hold only a single value, they can be cumbersome in programs that process lists of data. For example, suppose you are asked to design a program that