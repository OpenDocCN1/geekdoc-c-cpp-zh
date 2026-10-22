
## Programming Exercises

1. Modify the rain program in Listing 10.7 so that it does the calculations using pointers instead of subscripts. (You still have to declare and initialize the array.)

2. Write a program that initializes an array-of-double and then copies the contents of the array into three other arrays. (All four arrays should be declared in the main program.) To make the first copy, use a function with array notation. To make the second copy, use a function with pointer notation and pointer incrementing. Have the first two functions take as arguments the name of the target array, the name of the source array, and the number of elements to be copied. Have the third function take as arguments the name of the target, the name of the source, and a pointer to the element following the last element of the source. That is, the function calls would look like this, given the following declarations:

```
double source[5] = {1.1, 2.2, 3.3, 4.4, 5.5};
double target1[5];
double target2[5];
double target3[5];
copy_arr(target1, source, 5);
copy_ptr(target2, source, 5);
copy_ptrs(target3, source, source + 5);
```

3. Write a function that returns the largest value stored in an array-of-int. Test the function in a simple program.

4. Write a function that returns the index of the largest value stored in an array-of-double. Test the function in a simple program.

5. Write a function that returns the difference between the largest and smallest elements of an array-of-double. Test the function in a simple program.

6. Write a function that reverses the contents of an array of double and test it in a simple program.

7. Write a program that initializes a two-dimensional array-of-double and uses one of the copy functions from exercise 2 to copy it to a second two-dimensional array. (Because a two-dimensional array is an array of arrays, a one-dimensional copy function can be used with each subarray.)

8. Use a copy function from Programming Exercise 2 to copy the third through fifth elements of a seven-element array into a three-element array. The function itself need not be altered; just choose the right actual arguments. (The actual arguments need not be an array name and array size. They only have to be the address of an array element and a number of elements to be processed.)

9. Write a program that initializes a two-dimensional 3×5 array-of-double and uses a VLA-based function to copy it to a second two-dimensional array. Also provide a VLA-based function to display the contents of the two arrays. The two functions should be capable, in general, of processing arbitrary N×M arrays. (If you don’t have access to a VLA-capable compiler, use the traditional C approach of functions that can process an N×5 array.)

10. Write a function that sets each element in an array to the sum of the corresponding elements in two other arrays. That is, if array 1 has the values 2, 4, 5, and 8 and array 2 has the values 1, 0, 4, and 6, the function assigns array 3 the values 3, 4, 9, and 14. The function should take three array names and an array size as arguments. Test the function in a simple program.

11. Write a program that declares a 3×5 array of int and initializes it to some values of your choice. Have the program print the values, double all the values, and then display the new values. Write a function to do the displaying and a second function to do the doubling. Have the functions take the array name and the number of rows as arguments.

12. Rewrite the rain program in Listing 10.7 so that the main tasks are performed by functions instead of in main().

13. Write a program that prompts the user to enter three sets of five double numbers each. (You may assume the user responds correctly and doesn’t enter non-numeric data.) The program should accomplish all of the following:

    a. Store the information in a 3×5 array.
    b. Compute the average of each set of five values.
    c. Compute the average of all the values.
    d. Determine the largest value of the 15 values.
    e. Report the results.

    Each major task should be handled by a separate function using the traditional C approach to handling arrays. Accomplish task “b” by using a function that computes and returns the average of a one-dimensional array; use a loop to call this function three times. The other tasks should take the entire array as an argument, and the functions performing tasks “c” and “d” should return the answer to the calling program.

14. Do Programming Exercise 13, but use variable-length array function parameters.

## Character Strings and String Functions

You will learn about the following in this chapter:

- Functions:
  `gets(), gets_s(), fgets(), puts(), fputs(), strcat(), strncat(), strcmp(), strncmp(), strcpy(), strncpy(), sprintf(), strchr()`
- Creating and using strings
- Using several string and character functions from the C library and creating your own string functions
- Using command-line arguments

The character string is one of the most useful and important data types in C. You have been using character strings all along, but there still is much to learn about them. The C library provides a wide range of functions for reading and writing strings, copying strings, comparing strings, combining strings, searching strings, and more. This chapter will add these capabilities to your programming skills.

### Representing Strings and String I/O

Of course, you already know the most basic fact: A character string is a char array terminated with a null character (\0). Therefore, what you’ve learned about arrays and pointers carries over to character strings. But because character strings are so commonly used, C provides many functions specifically designed to work with strings. This chapter discusses the nature of strings, how to declare and initialize strings, how to get them into and out of programs, and how to manipulate strings.

Let’s look at a short program (see Listing 11.1) that illustrates some of the ways to represent strings in a program.

### Listing 11.1 The strings1.c Program

```
// strings1.c
#include <stdio.h>
#define MSG "I am a symbolic string constant."
#define MAXLENGTH 81
int main(void)
{
    char words[MAXLENGTH] = "I am a string in an array.";
    const char * pt1 = "Something is pointing at me.";
    puts("Here are some strings:");
    puts(MSG);
    puts(words);
    puts(pt1);
    words[8] = 'p';
    puts(words);
    return 0;
}
```

The puts() function, like printf(), belongs to the stdio.h family of input/output functions. It only displays strings, and, unlike printf(), it automatically appends a newline to the string it displays. Here’s the output:

```
Here are some strings:
I am a symbolic string constant.
I am a string in an array.
Something is pointing at me.
I am a spring in an array.
```

Rather than going through Listing 11.1 line-by-line, let’s take a more encompassing approach. First, we will look at ways of defining a string within a program. Then we will see what is involved in reading a string into a program. Finally, we will study ways to output a string.

### Defining Strings Within a Program

As you probably noticed when you read Listing 11.1, there are many ways to define a string. The principal ways are using string constants, using char arrays, and using char pointers. A program should make sure there is a place to store a string, and we will cover that topic, too.

### Character String Literals (String Constants)

A string literal, also termed a string constant, is anything enclosed in double quotation marks. The enclosed characters, plus a terminating \0 character automatically provided by the compiler, are stored in memory as a character string. So "I am a symbolic string constant.", "I am a string in an array.", "Something is pointing at me.", and "Here are some strings:" all are string literals.
