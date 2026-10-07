# Chapter 4 Compound Types

![](bbox=[0.355, 0.112, 0.786, 0.323])

Many programs depend on string input, it's worthwhile to explore this topic further. We'll have to draw on some of the more advanced features of cin, which are described in Chapter 17, "Input, Output, and Files."

# Reading String Input Line at a Time

Reading string input a word at a time is not the most desirable choice. For instance, suppose a program asks the user to enter a city, and the user responds with New York or Sao Paulo. You would want the program to read and store the full names, not just New Sao. To be able to enter while phrases instead of single words as a string, you need a different approach to string input. Specifically, you need a line-oriented method instead of a word-oriented method. You are in luck, for the istream class, of which cin is an example, has some line-oriented member functions: getline() and get(). Both read an entire input line—that is, up until a newline character. However, getline() then discards the newline character, whereas get() leaves it in the input queue. Let's look at the details, beginning with get().

# Line-Oriented Input with getline ()

The getline() function reads a line, using the newline character transmitted by the Enter key to mark the end of input. You invoke this method using cin.getline() as a function call. The function takes two arguments. The first argument is the name of the target (that is, the array destined to hold the line of input), and the second argument is a limit on the number of characters to be read. If this limit is, say, 20, the function reads no more than 19 characters, leaving room to automatically add the newline character at the end. The getline() member function reads input when it reads this numeric limit or whichever comes first.

For example, suppose you want to use getline() to read a name into the 20-element array. You would use this call:

```
cin.getline(name,20);
```