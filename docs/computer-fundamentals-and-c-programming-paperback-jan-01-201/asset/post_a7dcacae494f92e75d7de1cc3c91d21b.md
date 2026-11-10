
## A2. FILL IN THE BLANKS

- 9.1 EOF is usually defined as ______ in the file ______.
- 9.2 Keyboard input is first stored in a ______ before it reaches the program.
- 9.3 The precompiled object code of a library function is stored in an ______.
- 9.4 A UNIX text file is ______ than its converted MSDOS file.
- 9.5 `printf` and `scanf` use a ______ number of arguments.
- 9.6 `stdin`, `stdout` and `stderr` represent three ______ that remain ______ as long as the program is running.
- 9.7 The ______ function puts back a character into the input stream.
- 9.8 The format specifier `%[^\n]` is used by the ______ function to match an entire ______.
- 9.9 The `%s` format specifier matches a ______ in `scanf` and a ______ in `printf`.

## A3. MULTIPLE-CHOICE QUESTIONS

- 9.1 The character representing EOF is (A) [Ctrl-d] for UNIX and [Ctrl-z] for MSDOS, (B) the same for MSDOS and UNIX, (C) [Ctrl-z] for UNIX and [Ctrl-d] for MSDOS, (D) [Ctrl-z] for both systems.
- 9.2 For converting a UNIX file to MSDOS/Windows format, the LF character must be (A) replaced with CR, (B) succeeded by CR, (C) preceded by CR, (D) succeeded by another LF.
- 9.3 The `scanf` function returns (A) the number of characters read, (B) the number of items successfully read, (C) 1 on success, (D) none of these.
- 9.4 The statement `scanf("%f", price);` (A) assigns a real number to price, (B) stores a real number at the address of price, (C) generates a compiler error, (D) interprets price as an address and attempts to store the input at the address.
- 9.5 The statement `scanf("%d%*d%f", &days, &price);` (A) generates a compilation error, (B) generates a runtime error, (C) reads an int and long into days and price, (D) reads first and third data items into days and price, respectively.
- 9.6 Pick the odd item out: (A) %f, (B) %u, (C) %d, (D) %ld.
- 9.7 The `printf` function returns (A) the number of words written, (B) the number of characters written, (C) 1 on success, (D) none of these.
- 9.8 The statement `printf("%f%f\n", f1, f2, f3);` (A) generates a compilation error, (B) prints f1 and f2 only, (C) prints f1, f2 and junk, (D) none of these.

## A4. MIX AND MATCH

- 9.1 Match the line-terminating characters with the operating system:
  (A) carriage return (CR), (B) linefeed (LF), (C) carriage return-linefeed (CR-LF).
  (1) UNIX, (2) MSDOS, (3) Mac OS X
- 9.2 Match each format specifier with the corresponding data type:
  (A) %d, (B) %f, (C) %ld, (D) %[^\n], (E) %o.
  (1) octal integer, (2) scan set, (3) real number, (4) signed integer, (5) long integer.

## CONCEPT-BASED QUESTIONS

- 9.1 Why does the `getchar` function return an `int` instead of a `char`?
- 9.2 What does the following sequence achieve? What is the significance of the `;` at the end of the second line?
    ```c
    scanf("%c", &reply);
    while (getchar() != '\n');
    ```
- 9.3 What is the limitation of the following statement? Which format specifier will you use to overcome it?
    ```c
    scanf("%s", arr);
    ```
- 9.4 Why does `scanf` use addresses of variables as arguments even though `printf` doesn’t?
- 9.5 What is the difference in the data conversion techniques employed by `scanf` and `printf`?

## PROGRAMMING & DEBUGGING SKILLS

- 9.1 Write a program that uses `getchar` to accept any string but uses `putchar` to print only the uppercase letters separated by spaced dots.
- 9.2 Modify the preceding program in C.9.1 to use only `getc` and `putc`. How can you run this program from the shell of the operating system?
- 9.3 Use `getchar` and `switch` in a program to accept from the keyboard a string comprising only letters and then print the number of vowels and consonants in the string.
- 9.4 Develop a menu-based program that first prompts for an integer and then presents three options of printing that number in octal, decimal or hex.
- 9.5 Write a program that uses `scanf` to accept a time in `HH:MM:SS` 24-hour format. The three components must be validated before they are printed in the new format: `HH` hours, `MM` minutes, `SS` seconds.
- 9.6 The statement `printf("%d\f\n");` doesn’t print the six-character string enclosed within quotes. Correct the statement.
- 9.7 Write a program that repeatedly asks for a letter, validates the input and quits when the user enters 0. The program should reverse the case of the letter before printing it and its ASCII value. (Make sure the buffer doesn’t create problems.)
- 9.8 Write a program to accept a floating point number from the keyboard. Print the same number in the following formats: (i) total width of 10 characters, (ii) as in (i) but with 3 places after decimal, (iii) exponential notation, (iv) as in (iii) but with 3 places after decimal.
- 9.9 The following sequence is meant to print the string Jan, but it doesn't. What change needs to be made for obtaining the correct output?
    ```c
    char s[10] = "JanFebMar";
    printf("%3s", s);
    ```
- 9.10 Write a program to print a truncated string that is defined in the program. The width of the truncated portion must be set by the user.
- 9.11 Use the * flag of printf in a program to print the pattern shown below. The number of rows in the pattern (here, six) must be accepted from user input.
    ```
            *       *
             *     *
              *   *
               * *
                **
    ```

## 10 Arrays

### WHAT TO LEARN

- Techniques of initializing a single-dimensional array.
- Populating an array with `scanf`.
- Inserting and deleting elements in an array.
- Reversing an array with and without using a second array.
- Understanding and implementing the *selection sort* algorithm.
- Searching an array using *sequential* and *binary search*.
- Handling two- and three-dimensional arrays.
- Applying the concepts of two-dimensional arrays to manipulate matrices.
- The C99 feature of determining the size of an array at runtime.

### 10.1 ARRAY BASICS

Variables can’t handle voluminous data because a hundred data items need a hundred variables to store them. The solution is to use an *array*, which is an ordered set of data items stored contiguously in memory. Each data item represents an *element* of the array and is accessed with an *index* or *subscript*. For instance, the elements of an array named signal are accessed as signal[0], signal[1], signal[2], and so forth. The first subscript is 0 and the last subscript is one less than the size of the array.

The elements of an array have a common data type (like int, char, etc.). An array must be declared with its type and size to enable the compiler to allocate a contiguous chunk of memory for all array elements. This is how an array named signal having 32 elements is declared:

```
int signal[32];
```

The first element is accessed as signal[0] and the last element is signal[31] (not 32). The subscript is either zero, a positive integer or an expression that evaluates to an integer value. An array element can be assigned to a variable (say, int x = signal[2];), which means we can use signal[2] wherever we use x. By the same logic, &signal[2] is also a valid scanf argument like &x. It is easy to cycle through all array elements by using the array subscript as a key variable in a loop.

C doesn’t offer bounds checking for arrays, i.e. it doesn’t validate the index used to access an array element. For instance, the compiler will not generate an error if you attempt to access signal[35] even though the array has 32 elements. A negative index (as in signal[-5]) doesn’t generate an error either. However, these accesses create problems at runtime because the program accesses an area of memory that was not allocated for the array. C trusts the programmer, so you’ll have to do the bounds checking yourself.

The data type of an array is not restricted to the fundamental ones. Even derived and user-defined types like pointers and structures can be stored in arrays. C also supports multi-dimensional arrays where an element is handled with multiple subscripts. Since there is virtually no limit to the number of indexes and dimensions an array can have, arrays in C are very powerful data structures that can easily gobble up a lot of memory.

Because arrays can save a lot of data using a single identifier, there are a number of useful things you can do with them. You can add or delete array elements, reverse an array, sort and search it as well. You can also make a frequency count of the items in an array. Furthermore, many of the routines we develop in this chapter deserve to be converted to functions, a task that we’ll attempt in Chapter 11.

> **Note:** C doesn’t complain if you use a negative index or one that exceeds its size. For instance, `rate[-2]` will clear the compilation phase but it will evaluate to an unpredictable value at runtime. It may destroy another variable, i.e., a part of the program you are running.

### 10.2 DECLARING AND INITIALIZING AN ARRAY

Like a variable, an array has to be declared before use. The declaration of an array specifies its name, type and size, which is normally specified as a constant or symbolic constant. The following statement declares a single-dimensional array named signal having 32 elements, each of type int:

```
int signal[32];  /* Size specified explicitly */
```

This declaration also defines the array by allocating the required memory where the last segment of memory is used by signal[31]. The sizeof operator, when used on an array, returns the total usage of all elements, so the above definition allocates 32 × sizeof(int) bytes of memory—typically, 128 bytes. Figure 10.1 depicts the memory layout of a single-dimensional array of 10 elements.

Arrays of other primitive data types are declared in a similar manner:

```
short months[12];  /* Unlikely to change size */
float rate[10];
char name[SIZE];  /* Uses symbolic constant */
```

The naming rules for variables (5.2.1) apply in identical manner to arrays. This means that the name of an array can comprise only letters, numerals and the underscore character, but it cannot begin with a digit. Also, case is significant, so months[12] and MONTHS[12] are two separate arrays.
