# Tip

# LINE BREAKS IN I/O

It is possible to keep output and input on the same line, and sometimes it can produce a nicer interface for the user. If you simply omit a \n or endl at the end of the last prompt line, then the user's input will appear on the same line as the prompt. For example, suppose you use the following prompt and input statements:

```
cout << "Enter the cost per person: $";
 cin >> costPerPerson;
```

When the cout statement is executed, the following will appear on the screen:

Enter the cost per person: $

When the user types in the input, it will appear on the same line, like this:

Enter the cost per person: $1.25

# Self-Test Exercises

+   9. Give an output statement that will produce the following message on the screen.
+   The answer to the question of
+   Life, the Universe, and Everything is 42.

+   10. Give an input statement that will fill the variable theNumber (of type int) with a number typed in at the keyboard. Precede the input statement with a prompt statement asking the user to enter a whole number.

+   11. What statements should you include in your program to ensure that when a number of type double is output, it will be output in ordinary notation with three digits after the decimal point?

+   12. Write a complete C++ program that writes the phrase Hello world to the screen. The program does nothing else.

+   13. Give an output statement that produces the letter 'A', followed by the newline character, followed by the letter 'B', followed by the tab character, followed by the letter 'C'.