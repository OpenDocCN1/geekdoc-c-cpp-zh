
7 declares two pointers and a character used later in the listing. None of these variables is initialized, so they shouldn't be used—yet!

The malloc() function is called in line 14 with a parameter of 35 multiplied by the size of a char. Could you have used 35? Yes, but you're assuming that everyone running this program will be using a computer that stores char type variables as 1 byte in size. Remember from Lesson 3 that different compilers use different-size variables. Using the sizeof operator is easy to create portable code.

Never assume that malloc() gets the memory you tell it to get. In fact, you're not telling it to get memory—you're asking it. Line 16 shows how to check whether malloc() provided. If the memory was allocated, ptr points to it; otherwise, ptr is null. If the program failed to get the memory, lines 18 and 19 display an error message and gracefully exit the program.

Line 29 initializes the other pointer declared on line 7, p. It is assigned the same address value as ptr. A for loop uses this new pointer to place values in the allocated memory. Looking at line 31, we see that count is initialized to 65 and incremented by 1 until it reaches. For each loop of the for statement, the value of count is assigned to the address pointed to by p. Notice that each time count is incremented, the address pointed to by p is also incremented. This means that each value is placed one after the other in memory.

You should have noticed that numbers are assigned to count, which is a type char variable. Remember the discussion of ASCII characters and their numeric equivalents? The number 65 is equivalent to A, 66 b, 67 c, and so on. The for loop ends after the character assigned to the memory locations pointed to. Line 36 caps off the character values pointed to by putting a null at the final address pointed to by p. By appending the null, you can now use these values as a string. Remember that ptr points to the first value, A, so if you use it as a string, it prints every character until it reaches null. Line 40 uses puts() to prove this and to show the results of what has been done.

You can notice a new function is used on line 42. This is the free() function. Whenever you allocate memory dynamically, you should also deallocate it—or return it—when you finish using it. The free function returns allocated memory, so on line 42, the memory allocated and assigned to ptr is returned to the system.

# LESSON 10 Working with Characters and Strings

| DO | DON'T |
|---|---|
| | DON'T allocate more memory than you need. Not everyone has a lot of memory, so you should try to use it sparsely. |
| | DON'T try to assign a new string to a character array that was previously allocated only enough memory to hold a smaller string. For example, in this declaration:

```c
char a_string[] = "NO";
```

a_string points to "NO". If you try to assign "YES" to this array, you could have serious problems. The array initially could hold only three characters—'N', 'O', and a null. "YES" is four characters—'Y', 'E', 'S', and a null. You have no idea the fourth character, null, overwritten.

# Displaying Strings and Characters

If your program uses string data, it probably needs to display the data on the screen at some time. String display is usually done with either the puts() function or the printf() function.

# The puts() Function

You've already seen the puts() library function in some of the programs earlier in this book. The puts() function puts a string onscreen—hence its name. A pointer to the string to be displayed is the only argument puts() takes. Because a literal evaluates as a pointer to a string, puts() can be used to display literal string as well as string variables. The puts() function automatically inserts a newline character at the end of each string it displays, so each subsequent string displayed with puts() is on its own line.

Listing 10.4 illustrates the use of puts().

# Displaying Strings and Characters

# LISTING 10.4 put:c: Using the puts() Function to Display Text Onscreen

```c
1: /* demonstrates displaying strings with puts(). */
3: #include <stdio.h>
4: 
5: char *message1 = "C";
6: char *message2 = "is the";
7: char *message3 = "best";
8: char *message4 = "programming";
9: char *message5 = "language!";
10: 
11: int main( void )
12: {
13: puts(message1);
14: puts(message2);
15: puts(message3);
16: puts(message4);
17: puts(message5);
18: 
19: return 0;
20: }
```

# Output

```
c
is is the
best
programming
language!!
```

# Analysis

This is a fairly simple listing to follow. Because puts() is a standard output function, the stdio.h header file needs to be included, as done on line 3. Lines 5 through 9 declare and initialize five different variables. Each of these variables is a character pointer, or string variable. Lines 13 through 17 use the puts() function to print each string.

# The printf() Function

You can also display strings using the printf() library function. Recall from Lesson 7 that printf() uses a format string to display data.

Because a literal evaluates as a pointer to a string, puts() can be used to display literal string as well as string variables. The puts() function automatically inserts a newline character at the end of each string it displays, so each subsequent string displayed with puts() is on its own line.

# Displaying Strings and Characters

# LESSON 10 Working with Characters

# Displaying Strings and Characters

# The printf() Function

You can also display strings using the printf() library function. Recall from Lesson 7 that printf() uses a format string to display data.

Because a literal evaluates as a pointer to a string, puts() can be used to display literal string as well as string variables. The puts() function automatically inserts a newline character at the end of each string it displays, so each subsequent string displayed with puts() is on its own line.

# Reading Strings from the Keyboard

In addition to displaying strings, programs often need to accept string data from the keyboard. The C library has two functions that can be used for this: gets() and scanf(). Before you can read a string from the keyboard, however, you must have where to put it. You can create space for string storage using either of the methods—an array declaration or the malloc() function.

# Inputting Strings Using gets() Function

The gets() function gets a string from the keyboard. When gets() is called, it reads all characters typed at the keyboard up to the newline character (which you generate by pressing Enter). This function discards the newline, adds a null character, and gives the string to the calling program. The string is stored at the location indicated by a pointer to char passed to gets(). A program that uses gets() must include the file stdio.h. Listing 10.5 presents an example.

# Reading Strings from the Keyboard

# Input

LISTING 10.5 get.c: Using gets() to Input String Data from the Keyboard

```c
/* Demonstrates using the gets() library function. */
2:
3 #include <stdio.h>
4: 
5 /* Allocate a character array to hold input. */
6: 
7 char input[257];
8: 
9 int main( void )
10: {
11: puts("Enter some text, then press Enter: ");
12: gets(input);
13: printf("You entered: %s\n", input);
14: 
15: return 0;
16: }
```

# Output

```
Enter some text, then press Enter:
**This is a test**
You entered: This is a test
```

# Analysis

In this example, the argument to gets() is the expression input, which is the name of a type char array and therefore a pointer to the first array element. The array is declared with 257 elements in line 7. Because the maximum length possible on computer screens is 256 characters, this array provides space for the longest possible input line (plus the null character that gets() adds at the end).

The gets() function has a return value, which is gets() returns a pointer to type char with the address where the input string is stored. Yes, this is the same value that is passed to gets(), but having the value returned to the program in this way lets your program test for a blank line. Listing 10.6 shows how to do this.
