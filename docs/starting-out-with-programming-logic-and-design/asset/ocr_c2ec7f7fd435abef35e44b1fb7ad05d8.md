# Chapter 2 Input, Processing, and Output

data from the keyboard with the Input statement. As an example, look at the follow- ing statement, which appeared earlier in the pay calculating program:

# Input hours

The word Input is an instruction to read a data from the keyboard. The word is the name of the variable in which that data will be stored. When this state- executes, two things happen:

+   * The program waits and for the user to type something on the keyboard, and then press the Enter key.
* When the Enter key is pressed, the data that was typed is stored in the hours variable.

Program 2-2 is a simple pseudocode that demonstrates the Input statement. Before we examine the program, we should mention a couple of things. First, you will notice each line in the program is numbered. The line numbers are not part of the pseudocode. We will refer to the line numbers to point out specific parts of the program. Second, the program's output is shown immediately following the pseudoc- od. From now on, all pseudocode programs will be shown this way.

# Program 2-2

```
1 Display "What is your age?"
2 Input age
3 Display "Here is the value that you entered:"
4 Display age
```

# Program Output (with Input Shown in Bold)

What is your age?
24 [Enter]
Here is the value that you entered:
24

The statement in line 1 displays the string "What is your age?" Then, the statement in line 2 waits for the user to type a value on the keyboard and press Enter. The value that will be stored in the age variable. In the example execution of the program, the user has entered 24. The statement in line 3 displays the "here is the value that you entered" and the statement in line 4 displays the data that is stored in the age variable.

Notice that in line 4 there are no quotation marks around age. If quotation marks were placed around the age variable, it would have indicated that we to display the word age instead of the contents of the age variable. In other words, the display statement is an instruction to display the contents of the age variable:

# Display age

This statement, however, is an instruction to display the word age:

# Display "age"

> NOTE: In this section, we have mentioned the user. The user is simply any hypo-thetical person that is using a program and providing input for it. The user is some- called the end user.