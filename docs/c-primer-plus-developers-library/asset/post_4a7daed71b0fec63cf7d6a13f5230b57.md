
when the block containing it (typically a function definition) is entered, and it expires when the block is left. A static variable persists for the duration of a program. The Standard Template Library (STL), added by the C++98 standard, provides a vector template class that provides an alternative to do-it-yourself dynamic arrays. C++11 provides an array template class that offers an alternative to fixed-sized built-in arrays.

### Chapter Review

- 1. How would you declare each of the following?
  - a. actors is an array of 30 char.
  - b. betsie is an array of 100 short.
  - c. chuck is an array of 13 float.
  - d. dipsea is an array of 64 long double.
- 2. Does Chapter Review Question 1 use the array template class instead of built-in arrays?
- 3. Declare an array of five ints and initialize it to the first five odd positive integers.
- 4. Write a statement that assigns the sum of the first and last elements of the array in Question 3 to the variable even.
- 5. Write a statement that displays the value of the second element in the float array ideas.
- 6. Declare an array of char and initialize it to the string "cheeseburger".
- 7. Declare a string object and initialize it to the string "Waldorf Salad".
- 8. Devise a structure declaration that describes a fish. The structure should include the kind, the weight in whole ounces, and the length in fractional inches.
- 9. Declare a variable of the type defined in Question 8 and initialize it.
- 10. Use enum to define a type called Response with the possible values Yes, No, and Maybe. Yes should be 1, No should be 0, and Maybe should be 2.
- 11. Suppose ted is a double variable. Declare a pointer that points to ted and use the pointer to display ted's value.
- 12. Suppose treacle is an array of 10 floats. Declare a pointer that points to the first element of treacle and use the pointer to display the first and last elements of the array.
- 13. Write a code fragment that asks the user to enter a positive integer and then creates a dynamic array of that many ints. Do this by using new, then again using a vector object.
- 14. Is the following valid code? If so, what does it print?

```cpp
cout << (int *) "Home of the jolly bytes";
```

- 15. Write a code fragment that dynamically allocates a structure of the type described in Question 8 and then reads a value for the kind member of the structure.
- 16. Listing 4.6 illustrates a problem created by following numeric input with line-oriented string input. How would replacing this:

```cpp
cin.getline(address, 80);
```

with this:

```cpp
cin >> address;
```

affect the working of this program?

- 17. Declare a `vector` object of 10 `string` objects and an array object of 10 `string` objects. Show the necessary header files and don’t use `using`. Do use a `const` for the number of strings.

### Programming Exercises

- 1. Write a C++ program that requests and displays information as shown in the following example of output:

```text
What is your first name? Betty Sue
What is your last name? Yewe
What letter grade do you deserve? B
What is your age? 22
Name: Yewe, Betty Sue
Grade: C
Age: 22
```

Note that the program should be able to accept first names that comprise more than one word. Also note that the program adjusts the grade downward—that is, up one letter. Assume that the user requests an A, a B, or a C so that you don’t have to worry about the gap between a D and an F.

- 2. Rewrite Listing 4.4, using the C++ `string` class instead of `char` arrays.
- 3. Write a program that asks the user to enter his or her first name and then last name, and that then constructs, stores, and displays a third string, consisting of the user’s last name followed by a comma, a space, and first name. Use `char` arrays and functions from the `cstring` header file. A sample run could look like this:

```text
Enter your first name: Flip
Enter your last name: Fleming
Here’s the information in a single string: Fleming, Flip
```

- 4. Write a program that asks the user to enter his or her first name and then last name, and that then constructs, stores, and displays a third string consisting of the user’s last name followed by a comma, a space, and first name. Use string objects and methods from the string header file. A sample run could look like this:

```text
Enter your first name: Flip
Enter your last name: Fleming
Here’s the information in a single string: Fleming, Flip
```

- 5. The CandyBar structure contains three members. The first member holds the brand name of a candy bar. The second member holds the weight (which may have a fractional part) of the candy bar, and the third member holds the number of calories (an integer value) in the candy bar. Write a program that declares a structure and creates a CandyBar variable called snack, initializing its members to "Mocha Munch", 2.3, and 350, respectively. The initialization should be part of the declaration for snack. Finally, the program should display the contents of the snack variable.
- 6. The CandyBar structure contains three members, as described in Programming Exercise 5. Write a program that creates an array of three CandyBar structures, initializes them to values of your choice, and then displays the contents of each structure.
- 7. William Wingate runs a pizza-analysis service. For each pizza, he needs to record the following information:
  - The name of the pizza company, which can consist of more than one word
  - The diameter of the pizza
  - The weight of the pizza

Devise a structure that can hold this information and write a program that uses a structure variable of that type. The program should ask the user to enter each of the preceding items of information, and then the program should display that information. Use *cin* (or its methods) and *cout*.

- 8. Do Programming Exercise 7 but use new to allocate a structure instead of declaring a structure variable. Also have the program request the pizza diameter before it requests the pizza company name.
- 9. Do Programming Exercise 6, but instead of declaring an array of three CandyBar structures, use new to allocate the array dynamically.
- 10. Write a program that requests the user to enter three times for the 40-yd dash (or 40-meter, if you prefer) and then displays the times and the average. Use an array object to hold the data. (Use a built-in array if array is not available.)

This page intentionally left blank

## Loops and Relational Expressions

In this chapter you’ll learn about the following:

- The for loop
- Expressions and statements
- The increment and decrement operators: ++ and --
- Combination assignment operators
- Compound statements (blocks)
- The comma operator
- Relational operators: >, >=, ==, <=, <, and !=
- The while loop
- The typedef facility
- The do while loop
- The get() character input method
- The end-of-file condition
- Nested loops and two-dimensional arrays

Computers do more than store data. They analyze, consolidate, rearrange, extract, modify, extrapolate, synthesize, and otherwise manipulate data. Sometimes they even distort and trash data, but we’ll try to steer clear of that kind of behavior. To perform their manipulative miracles, programs need tools for performing repetitive actions and for making decisions. Of course, C++ provides such tools. Indeed, it uses the same for loops, while loops, do while loops, if statements, and switch statements that regular C employs, so if you know C, you can zip through this chapter and Chapter 6, “Branching Statements and Logical Operators.” (But don’t zip too fast—you don’t want to miss how cin handles character input!) These various program control constructs often use relational expressions and logical expressions to govern their behavior. This chapter discusses
