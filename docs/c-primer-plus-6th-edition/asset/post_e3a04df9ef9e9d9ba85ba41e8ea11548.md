
# Summary

If you intended for the strings to be modifiable, you would omit the const qualifier. This form uses the initializer list and the same for for loop display code as the other two forms. If you want modifiable strings, the automatic sizing feature of the string class makes this approach more convenient to using the two-dimensional array approach.

# Summary

C++ offers three varieties of loops: for loops, while loops, and do-loops. A loop cycles through the same set of instructions repetitively, as long as the loop condition evaluates to true or nonzero and the loop terminates execution when the condition evaluates to false or zero. The for loop and the while loop are entry-condition loops, meaning that they examine the test condition before executing the statements in the body of the loop. The do loop is an exit-condition loop, meaning that it examines the test after executing the statements in the body of the loop.

The syntax for each loop calls for the loop body to consist of a single statement. However, that can be a compound statement, or block, formed by enclosing several statements within paired braces.

Relational expressions, which compare two values, are often used as loop test conditions. Relational expressions are formed by using one of the relational operators: <, <=, ==, >=, >, or !=. Relational expressions evaluate to the type bool true and false.

Many programs read input or text files character-by-character. The istream class provides several ways to do this. If ch is a type char variable, the following statement reads the next input character into ch:

```cpp
cin >> ch;
```

However, it skips over spaces, newlines, and tabs. The member function call reads the next input character, regardless of its value, and places it in ch:

```cpp
cin.get(ch);
```

The member function cin.get() returns the next input character, including spaces, newlines, and tabs, so it can be used as follows:

The cin.get(char) member function reports encountering the EOF condition by returning a value with the bool conversion of false, whereas the cin.get() member function call reports the EOF by returning the value EOF, which is defined in the istream file.

```cpp
iostream
```

A nested loop is a loop within a loop. Nested loops provide a natural way to process two-dimensional arrays.

## Chapter 5 Loops and Relational Expressions

# Chapter Review

- 1. What's the difference between an entry-condition loop and an exit-condition loop? Which kind is each of the C++ loops?

- 2. What would the following code fragment print if it were part of a valid program?
```cpp
int i;
for (i = 0; i < 5; i++)
cout << i;
cout << endl;
```

- 3. What would the following code fragment print if it were part of a valid program?
```cpp
int j;
for (j = 0; j < 11; j += 3)
cout << j;
cout << endl << j << endl;
```

- 4. What would the following code fragment print if it were part of a valid program?
```cpp
int j = 5;
while (+j < 9)
cout << j++ << endl;
```

- 5. What would the following code fragment print if it were part of a valid program?
```cpp
int k = 8;
do
cout << "k = " << k << endl;
while (k++ < 5);
```

- 6. Write a loop that prints the values 1 2 4 8 16 32 64 by increasing the value of a counting variable by a factor of two in each cycle.

- 7. How do you make a loop body include more than one statement?

- 8. Is the following statement valid? If not, why not? If so, what does it do?
```cpp
int x = (1,024);
What about the following?
int y;
y = 1,024;
```

- 9. How does cin>>ch differ from cin.get(ch) and ch=cin.get() in how it views input?

# Programming Exercises

- 1. Write a program that requests the user to enter two integers. The program should then calculate and report the sum of all the integers between and including the two integers. At this point, assume that the smaller is entered first. For example, if the user enters 2 and 9, the program should report that the sum of all the integers from 2 through 9 is 44.

- 2. Redo Listing 5.4 using a type array instead of a built-in array and type long double instead of long int. Find the value of 100!.

- 3. Write a program that asks the user to enter in numbers. After each entry, the program should report the cumulative sum of the entries to date. The program should terminate when the user enters 0.

- 4. Daphne invests $100 at 10% simple interest. That is, every year, the investment earns 10% of the original investment, or $10 each and every year:

```cpp
interest = 0.10 * original balance
```

Cleo invests $100 at 10% compound interest. That is, every year, the investment earns 10% of the current balance, or $10 each and every year:

```cpp
interest = 0.10 * current balance
```

Daphne invests $100 at 10% simple interest. That is, every year, the investment earns 10% of the original investment, or $10 each and every year:

```cpp
interest = 0.10 * original balance
```

Cleo invests $100 at 10% compound interest. That is, every year, the investment earns 10% of the current balance, or $10 each and every year:

```cpp
interest = 0.10 * current balance
```

Daphne invests $100 at 10% simple interest. That is, every year, the investment earns 10% of the original investment, or $10 each and every year:

```cpp
interest = 0.10 * original balance
```

Cleo invests $100 at 10% compound interest. That is, every year, the investment earns 10% of the current balance, or $10 each and every year:

```cpp
interest = 0.10 * current balance
```

Daphne invests $100 at 10% simple interest. That is, every year, the investment earns 10% of the original investment, or $10 each and every year:

```cpp
interest = 0.10 * original balance
```

Cleo invests $100 at 10% compound interest. That is, every year, the investment earns 10% of the current balance, or $10 each and every year:

```cpp
interest = 0.10 * current balance
```

- 5. Write a program that asks the user to enter in numbers. After each entry, the program should report the cumulative sum of the entries to date. The program should terminate when the user enters 0.

- 6. Daphne invests $100 at 10% simple interest. That is, every year, the investment earns 10% of the original investment, or $10 each and every year:

```cpp
interest = 0.10 * original balance
```

Cleo invests $100 at 10% compound interest. That is, every year, the investment earns 10% of the current balance, or $10 each and every year:

```cpp
interest = 0.10 * current balance
```

Daphne invests $100 at 10% simple interest. That is, every year, the investment earns 10% of the original investment, or $10 each and every year:

```cpp
interest = 0.10 * original balance
```

Cleo invests $100 at 10% compound interest. That is, every year, the investment earns 10% of the current balance, or $10 each and every year:

```cpp
interest = 0.10 * current balance
```

- 7. Design a structure called car that holds the following information: its make, a string, and the year it was built. Write a program that asks the user how many cars you wish to catalog? The program should then use new to create a dynamic array and display the contents of each structure. A sample run should look like the following:

```
How many cars do you wish to catalog? 2
Car #1:
Please enter the make: Hornet
Please enter the year made: 1952
Car #2:
Please enter the make: Kaiser
Please enter the year made: 1951
Here is your collection:
1952 Hornet
1951 Kaiser
```

- 8. Write a program that uses an array of char and a loop to read one word at a time until the word is entered. The program should then report the number of words entered (not counting done). A sample run could look like this:

```
Enter words (to stop, type the word done):
anteater birthday category dumpster envy finagle for sure
You entered a total of 7 words.
```

- 9. Write a program that matches the description of Programming Exercise 8, but use string object instead of an array. Include the string header file and use a relational operator to make the comparison test.

- 10. Write a program using nested loops that asks the user to enter a value for the number of rows to display. It should display that many rows of asterisks, one asterisk in the first row, two in the second row, and so on. For each row, the asterisks are preceded by the number of periods needed to make all the rows display a total number of characters equal to the number of rows. A sample run would look like this:

```
Enter number of rows: 5

*...
**
***
****
*****
```

# Branching Statements and Logical Operators

In this chapter you'll learn about the following:

- The if statement
- The if else statement
- Logical operators: &&, ||, and !
- The cctype library of character functions
- The conditional operator: ?:
- The switch statement
- The continue and break statements
- Number-reading loops
- Basic file input/output

One of the keys to designing intelligent programs is to give them the ability to make decisions. Chapter 5, "Loops and Relational Expressions," shows one kind of decision making—in which a program decides whether to continue looping. This chapter investigates how C++ uses branching statements to decide among alternative actions. With vampire-protection scheme (garlic or cross) should the program use? What menu choice has the user selected? Did the user enter a zero? The if and switch statements to implement decisions, and they are this chapter's main topics. This chapter also looks at the conditional operator, which provides another way to make a choice, and the logical operators, which let you combine two tests into one. Finally, the chapter takes a first look at file input/output.
