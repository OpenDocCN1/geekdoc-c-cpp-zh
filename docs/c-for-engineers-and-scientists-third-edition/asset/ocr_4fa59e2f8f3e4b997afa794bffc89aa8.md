# Chapter 2 Arithmetic Operations 69

The spaces around arithmetic operators in these examples are inserted strictly for clarity and can be omitted without affecting the value of the expression. However, an expression in C++ must be entered in a straight-line form, as shown in these examples. For example, the C++ expression equivalent to 12.6 divided by 2 must be entered as 12.6 / 2 , not as as the algebraic expression shown here:

```
12.6
2
```

You can use count to display the value of any arithmetic expression onscreen. To do this, the value must be sent to the object. For example, the following statement displays the yield:

```
cout << (6 + 15);
```

*Strictly speaking, the parentheses surrounding the expression 6 + 15 are not required to indicate that the value of the expression (that, 21) is being displayed.* In addition to displaying a numerical value, count can display a string identifying the output, as was done in Section 2.1. For example, the following statement sends two pieces of data, a string and a value, to count:

```
cout << "sum of 6 and 15 is " << (6 + 15);
```

Each set of data to count must be preceded by its own insertion operator, <<. In the preceding example, the first data sent to display is the string " sum of 6 and 15 is", the second item is sent to the value of the expression 6 + 15. This statement produces the following:

The sum of 6 and 15 is 21

The space between the word "is" and the number 21 is caused by the space in the string sent to count. As far as count, its input is a set of characters to be displayed in the order they're received. Characters from the input are queued, one after the other, and to the screen they are received. Placing a space in the input makes the space part of the stream of characters that displayed. For example, the statement

```
cout << "sum of 12.2 and 15.754 is " << (12.2 + 15.754);
```

yields the following display:

The sum of 12.2 and 15.754 is 27.954

When multiple insertions are sent to count, the code can spread across multiple lines. Only one semicolon, must be used, which is placed after the last insertion and terminates the complete statement. Therefore, the preceding display is also produced by the following statement, which spans two lines:

```
cout << "sum of 12.2 and 15.754 is "
 << (12.2 + 15.754);
```

However, when you allow a statement to span multiple lines, two rules must be followed: a string contained in quotation marks cannot be split across lines, and the terminating semicolon should appear only on the last line. You can always place insertion symbols in a line.

> "The parentheses are not required because the + operator has a higher precedence than the << operator; therefore, the addition is performed before the insertion.