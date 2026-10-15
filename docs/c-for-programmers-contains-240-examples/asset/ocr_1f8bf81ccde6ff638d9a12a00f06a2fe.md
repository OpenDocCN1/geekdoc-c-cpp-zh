```
a = b = c = 0;
```

first evaluates the assignment c = 0 (because the = operator associates from right to left). The variable b is then assigned the value of the assignment c = 0 (which is 0). Then, the variable a is assigned the value of the assignment b = (c = 0) (which is also 0). In the program, the value of the assignment grade = cin.get() is compared with the value of EOF (a symbol whose acronym stands for “end-of-file”). We use EOF (which normally has the value −1) as the sentinel value. However, you do not type the value −1, nor do you type the letters EOF as the sentinel value. Rather, you type a system-dependent keystroke combination that means “end-of-file” to indicate that you have no more data to enter. EOF is a symbolic integer constant defined in the <iostream> header file. If the value assigned to grade is equal to EOF, the while loop (lines 60–100) terminates. We have chosen to represent the characters entered into this program as ints, because EOF has type int.

On UNIX/Linux systems and many others, end-of-file is entered by typing

```
<Ctrl> d
```

on a line by itself. This notation means to press and hold down the Ctrl key, then press the d key. On other systems such as Microsoft Windows, end-of-file can be entered by typing

```
<Ctrl> z
```

> [Note: In some cases, you must press Enter after the preceding key sequence. Also, the characters ^Z sometimes appear on the screen to represent end-of-file, as shown in Fig. 5.11.]

# Portability Tip 5.2

The keystroke combinations for entering end-of-file are system dependent.

# Portability Tip 5.3

Testing for the symbolic constant EOF rather than −1 makes programs more portable. The ANSI/ISO C standard, from which C++ adopts the definition of EOF, states that EOF is a negative integral value (but not necessarily −1), so EOF could have different values on different systems.

In this program, the user enters grades at the keyboard. When the user presses the Enter (or Return) key, the characters are read by the cin.get() function, one character at a time. If the character entered is not end-of-file, the flow of control enters the switch statement (lines 63–99), which increments the appropriate letter-grade counter based on the grade entered.

# switch Statement Details

The switch statement consists of a series of case labels and an optional default case. These are used in this example to determine which counter to increment, based on a grade. When the flow of control reaches the switch, the program evaluates the expression in the parentheses (i.e., grade) following keyword switch (line 63). This is called the controlling expression. The switch statement compares the value of the controlling expression with each case label. Assume the user enters the letter C as a grade. The program compares C to each case in the switch. If a match occurs (case 'C': in line 75), the program executes the statements for that case. For the letter C, line 77 increments cCount by 1. The break