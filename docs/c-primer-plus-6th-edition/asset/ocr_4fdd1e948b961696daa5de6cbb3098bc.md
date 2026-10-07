# Summary

If you intended for the strings to be modifiable, you would omit the const qualifier. This form uses the initializer list and the same for for loop display code as the other two forms. If you want modifiable strings, the automatic sizing feature of the string class makes this approach more convenient to using the two-dimensional array approach.

# Summary

C++ offers three varieties of loops: for loops, while loops, and do loops. A loop cycles through the same set of instructions repetitively, as long as the loop condition evaluates to true or nonzero and the loop terminates execution when the condition evaluates to false or zero. The for loop and the while loop are entry-condition loops, meaning that they examine the test condition before executing the statements in the body of the loop. The do loop is an exit-condition loop, meaning that it examines the test after executing the statements in the body of the loop.

The syntax for each loop calls for the loop body to consist of a single statement. However, that can be a compound statement, or block, formed by enclosing several statements within paired braces.

Relational expressions, which compare two values, are often used as loop test conditions. Relational expressions are formed by using one of the relational operators: <, <=, ==, >=, >, or !=. Relational expressions evaluate to the type bool true and false.

Many programs read input or text files character-by-character. The istream class provides several ways to do this. If ch is a type char variable, the following statement reads the next input character into ch:

```
cin >> ch;
```

However, it skips over spaces, newlines, and tabs. The member function call reads the next input character, regardless of its value, and places it in ch:

```
cin.get(ch);
```

The member function cin.get() returns the next input character, including spaces, newlines, and tabs, so it can be used as follows:

The cin.get(char) member function reports encountering the EOF condition by returning a value with the bool conversion of false, whereas the cin.get() member function call reports the EOF by returning the value EOF, which is defined in the istream file.

```
iostream
```

A nested loop is a loop within a loop. Nested loops provide a natural way to process two-dimensional arrays.