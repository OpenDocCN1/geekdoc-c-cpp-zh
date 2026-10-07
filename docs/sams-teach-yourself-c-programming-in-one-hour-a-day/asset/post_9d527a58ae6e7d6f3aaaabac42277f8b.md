
# 634 APPENDIX D Answers

- 3. An infinite loop executes forever. You create one by writing a for, do...while, or while loop with a test condition that is always true.

- 4. Execution terminates when the program reaches the end of main() or the exit() function is called.

- 5. The expression in a switch statement can evaluate to a long, int, or char value.

- 6. The default statement is a case in a switch statement. When the expression in the switch evaluates to a value that doesn't have a matching case, control goes to the default case.

- 7. The exit() function causes the program to end. A value can be passed to the exit() function. This value is returned to the operating system.

# Exercises

- 1. continue;

- 2. break;

- 3. This code fragment is correct. You don't need a break statement after the printf() for 'N', the switch statement ends anyway.

- 4. You might think that the default needs to go to the bottom of the switch statement, but this isn't true. The default can go anywhere. There is a problem, however- there should be a break statement at the end of the default case.

- 5. The code is as follows:

```c
if ( choice == 1 )
    printf("You answered 1");
else if( choice == 2 )
    printf("You answered 2");
    printf("You did not choose 1 or 2");
```

- 6. The code is as follows:

```c
do {
    /* any C statements */
} while ( 1 );
```

# Answers for Lesson 14

# Quiz

- 1. A stream is a sequence of bytes. A C program uses streams for all input and output.

- 2. a printer is an output device.

- b. A keyboard is an input device.

- c. A modem is both an input and an output device.

- d. a monitor is an output device. (Although a touch screen would be an input device and an output device.)

- e. a flash drive can be both an input and an output device.

- 3. All C compilers support three predefined streams: stdin (the keyboard), stdout (the screen), and stderr (the screen).

- 4. stdout

- b. stdout

- c. stdin

- d. stdin

- c. fprintf() can use any output stream. Of the three universal streams, it can use stdout and stderr.

- 5. Buffered input is sent to the program only when the user presses Enter. Unbuffered input is sent one character at a time, as soon as each key is pressed.

- 6. Echoed input automatically sends each character to stdout as it is received; unechoed input does not.

- 7. You can "unget" only one character between reads. The EOF character can't be put back into the input stream with unget().

- 8. With the newline character, which corresponds to the user pressing Enter.

- 9. a. Valid
- b. Valid
- c. Valid
- d. Not valid. There is not an identifier of q.

- e. Valid
- f. Valid

- 10. stderr shouldn't be redirected; it should always print to the screen. stdout can be redirected to somewhere other than the screen.

# Exercises

- 1. printf("Hello World" );

- 2. fprintf( stdout, "Hello World" );

```c
puts("Hello World");
```

- 3. The code is as follows:
```c
char buffer[31];
scanf("%30[*]", buffer);
```

- 4. The code is as follows:
```c
printf("Jack asked, \"What is a backslash?\"\nJill said, \\nIt is \\\\\\\''");
```

# Answers for Lesson 15

## Quiz

- 1. The code is as follows:
```c
float x;
float *px = &x;
float **ppx = &px;
```

- 2. The error that the statement uses a single indirection operator and, as a result, assigns the value 100 to px instead of x. The statement should be written with a double indirection operator:
```c
**ppx = 100;
```

- 3. array is a 3-D array with two elements. Each of these elements is itself an array that contains three elements. Each of these elements is an array that contains four type int variables.

- 4. array[0] is a pointer to the first four-element array of type int.

- 5. The first and third comparisons are true; the second is not true.

- 6. void func(char *p[]);

- 7. It has no way of knowing. This value must be passed to the function as another argument.

- a. var1 is a pointer to an integer.

- b. var2 is an integer.

- c. var3 is a pointer to a pointer to an integer.

- 9. a. a is an array of 36 (3x12) integers.

- b. b is a pointer to an array of 12 integers.
- c. c is an array of 12 pointers to integers.

# Exercises

- 1. char *ptrs[10];

- 2. ptr is declared as an array of 12 pointers to integers, not a pointer to an array of 12 integers. The correct code is:
```c
int x[3] [12];
int (*ptr) [12];

ptr = x;
```

# Answers for Lesson 16

# Quiz

- 1. A pointer to a function is a variable that holds the address where the function is stored in memory.

- 2. char (*ptr) (char *x[]);

- 3. If you omit the parentheses surrounding *ptr, the type is a prototype of a function that returns a pointer to type char.

- 4. The structure must contain a pointer to the same type of structure.

- 5. It means that the linked list is empty.

- 6. Each element in the list contains a pointer that identifies the next element in the list. The first element in the list is identified by the head pointer.

- 7. a. z is an array of 10 pointers to characters.

- b. y is a function that takes an integer (field) as an argument and returns a pointer to a character.

- c. x is a pointer to a function that takes an integer (field) as an argument and returns a character.

# Exercises

- 1. void func(char *p[]);
- 2. int func(int);
- 3. The linked list is empty.
- 4. The first element in the list is identified by the head pointer.
- 5. a. z is an array of 10 pointers to characters.
- b. y is a function that takes an integer (field) as an argument and returns a pointer to a character.
- c. x is a pointer to a function that takes an integer (field) as an argument and returns a character.
- 6. The structure must contain a pointer to the same type of structure.
- 7. It means that the linked list is empty.
- 8. Each element in the list contains a pointer that identifies the next element in the list.
- 9. The first element in the list is identified by the head pointer.
- 10. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 11. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 12. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 13. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 14. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 15. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 16. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 17. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 18. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 19. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 20. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 21. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 22. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 23. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 24. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 25. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 26. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 27. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 28. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 29. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 30. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 31. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 32. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 33. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 34. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 35. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 36. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 37. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 38. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 39. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 40. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 41. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 42. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 43. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 44. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 45. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 46. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 47. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 48. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 49. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 50. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 51. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 52. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 53. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 54. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 55. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 56. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 57. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 58. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 59. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 60. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 61. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 62. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 63. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 64. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 65. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 66. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 67. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 68. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 69. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 70. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 71. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 72. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 73. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 74. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 75. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 76. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 77. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 78. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 79. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 80. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 81. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 82. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 83. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 84. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 85. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 86. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 87. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 88. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 89. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 90. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 91. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 92. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 93. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 94. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 95. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 96. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 97. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 98. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 99. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```

- 100. The code is as follows:
```c
struct node {
    int data;
    struct node *next;
};
```
