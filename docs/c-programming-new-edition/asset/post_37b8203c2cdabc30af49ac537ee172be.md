
```c
{
int i = 13; return (&i);
}
```

In this program the address of `i` is initialized and declared in the called function and returned to the caller function, which is assigned to `p`, and the value of `p` at the address of `i` is displayed using the `printf` statements.

## 6.9. TWO-DIMENSIONAL ARRAYS AND POINTERS

You have already been apprised about the 2-dimensional arrays in the session Arrays and you are aware that a 2-dimensional array has a row and a column and it is usually a matrix. Here you will be acquainted with the representation of the 2-dimensional array with respect to a pointer.

A 2-dimensional array is actually an assortment of 1-dimensional arrays. Therefore, one can define a two-dimensional array as a pointer to a group of contiguous 1-dimensional arrays.

The general format can be specified as follows:

```c
data_type (*ptrvar)[size];
```

According to the above format, `data_type` refers to the data type of the array, `ptrvar` is the name of the pointer variable. Notice the parentheses that surround the array name and the preceding asterisk in the pointer version of each declaration.

These parentheses must be present. Without them you would be defining an array of pointers rather than a pointer to a group of arrays, since these particular symbols (i.e., the square brackets and the asterisk) would normally be evaluated right to left.

- Example 6.2:

  ```c
  int (*a)[20];
  ```

In this `a` is defined to be a pointer to a group of contiguous, one-dimensional, 20-element integer arrays. Thus, `a` points to the first 20-element array, which is actually the first row (i.e., row 0) of the original two-dimensional array.

Similarly, `(a + 1)` points to the second 20-element array, which is the second row (row 1) of the original two-dimensional array, and so on, as illustrated below.

a (a + 1)

```c
int *p(int i);
```

Indicates a function that accepts an integer argument and returns a pointer to an integer. On the other hand, the declaration:

```c
int (*p)(int a);
```

Indicates a pointer to a function that accepts an integer argument and returns an integer. In this last declaration, the first pair of parentheses is used for nesting, and the second pair is used to indicate a function. The interpretation of more complex declarations can be increasingly troublesome.

For example, consider the declaration:

```c
int* (*p)(int (*a)[]);
```

In this declaration, `(*p)(....)` indicates a pointer to a function. Hence, `int *(*p)(....)` indicates a pointer to a function that returns a pointer to an integer. Within the last pair of parentheses (the function’s argument specification), `(*a)[]` indicates a pointer to an array. Therefore, `int (*a)[]` represents a pointer to an array of integers.

Putting the pieces together, `(*p)(int (*a)[])` represents a pointer to a function whose argument is a pointer to an array of integers. And finally, the entire declaration:

```c
int *(*p)(int (*a)[]);
```

Represents a pointer to a function that accepts a pointer to an array of integers as an argument and returns a pointer to an integer. Remember that a left parenthesis immediately following an identifier name indicates that the identifier represents a function. Similarly, a left square bracket immediately following an identifier name indicates that the identifier represents an array. Parentheses that identify functions and square brackets that identify arrays have a higher precedence than the unary indirection operator. Therefore, additional parentheses are required when declaring a pointer to a function or a pointer to an array.

## 6.12. DO’S AND DON’TS

- **Do’s:**
  - The `&` sign is used to find out the address of a particular variable in the memory.
  - The `*` sign is used to find the value at address and indicates a pointer variable.
  - The address of a variable is always a whole number.
  - Printing the value of `*(&i)` is the same as printing the value of `i`.
- **Don’ts:**
  - When you are using an array of pointers to strings, you cannot initialize the strings from the keyboard; you can initialize only at the time of declaration.

In pointer arithmetic you cannot perform the operations of multiplication and division. In the beginning of this session you had been briefed about the basics of pointers and their declaration. The different types of pointer variations were then dealt with, which included the pointer declaration, arithmetic, and comparison. Then two important types of dynamic memory allocation were learnt. The chemistry between pointers and arrays was dealt with. Then assigning a pointer to another pointer was discussed. The array connection with pointers and some extras on pointer declaration was observed.

## Going Over It Again:

### Fill in the blanks:

1. To find the address of a particular variable in the memory the __________ sign is used.
2. To find the value at address the __________ sign is used.
3. There are ________ methods of dynamic memory allocation.
4. The address of a variable is always a __________ number.

### State True or False:

1. In pointer arithmetic the multiplication operation can be performed.
2. The `calloc()` and `malloc()` are standard library functions.
3. A pointer variable can store the address of another pointer variable.
4. Printing the value of `*(&i)` is the same as printing the value of `i`.
5. Pointer comparison between two variables can be done when both the variables do not point to an object of the same data type.

### One Line Answers:

1. What are the three different pointer variations?
2. What is the difference between `calloc()` and `malloc()`?
3. What is meant by the address of a variable?

In line number 5, as you can see, the character array is initialized to the string in the quotations. The initialized string is entered into an array using the for loop in line number 9. Apart from initializing the `i` value to 0, the condition in the for loop is set such that the value of `str[i]` is not equal to 0, i.e., the string will be entered into the loop until there are no more characters to be entered and it encounters the null character.

To print the string in the array, the `printf` statement is given, which is shown in line number 11. You will also notice here that the format specifier is `%c` because a character array is being used.

## 7.3. INTERNAL REPRESENTATION OF STRINGS

After your initial stint with strings and having written your first program using strings, it would be reasonable to say that you must be aware of the internal representation of the strings. In this section you will get an overview of how these strings are stored in the memory. The string representation is no different from that of the integer arrays in the sense that all the characters that constitute the string are stored in contiguous memory locations. That is to say, the first character will be stored in the 0th position and the second in the 1st and so on.

The last character, as you know, is the null character. You will now see how the string is stored in the memory.

| Character | B | O | N | D | \0 |
|-----------|---|---|---|---|---|
| Address | 1234 | 1235 | 1236 | 1237 | 1238 |

As you can see, the string `"bond"` is stored in a sequential manner and each character occupies one byte, but the point to observe here is that the string is terminated with a null character.

Another word about the length of the string is that if the length of a string is predefined, i.e., the number of spaces in the memory to be reserved for the particular string, then the null character is placed immediately after the last character and the rest of the spaces reserved are left empty. E.g., if the string is declared as `char str[10] = "bond";` The representation of the above string would be in the following fashion.

![](img/c948b22e3869eae71cd653f0917e0009_120_0.png)

`B O N D \0`. As you can see, after the null character the rest of the spaces are lying empty and this is not a healthy sign for the programmer.
