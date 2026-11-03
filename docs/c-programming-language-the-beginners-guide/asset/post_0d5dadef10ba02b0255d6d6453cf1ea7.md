
```c
3 int main()
4 {
5 int age;
6
7 age = 34;
8 printf("The C language is over %d years old!\n", age);
9
10 return(0);
11 }
12
```

Save the modified then build and run it. As you will see, the program’s output reflects the new value.

Now, assign a new value to the variable in the code by adding two lines after line eight. First, assign the value 50 to the age variable:

```c
1 #include <stdio.h>
2
3 int main()
4 {
5 int age;
6
7 age = 34;
8 printf("The C language is over %d years old!\n", age);
9 age = 50;
10
11
12
13 return(0);
14 }
15
```

Second, type another printf function:

```c
1 #include <stdio.h>
2
3 int main()
4 {
5 int age;
6
7 age = 34;
8 printf("The C language is over %d years old!\n", age);
9 age = 50;
10 printf("The programmer is over %d years old\n", age);
11
12 return(0);
13 }
14
```

Save the above changes, then build and run the code. See how the *age* variable is used twice, but hold two different integer values. On your own, you can change this code once more. This time you can assign your own age to the age variable and simply add a printf statement to say how old you are.

Math can also be performed using variables. Take a look at the code below:

```c
1 #include <stdio.h>
2
3 int main()
4 {
5 int age;
6
7 age = 32;
8 printf("%s is %d years old!\n", "James", age);
9 printf("That's %d months!\n", age*12);
10
11 return(0);
12 }
13
```

In line seven, the value 32 is assigned to the integer variable. Edit the value to reflect your own age in years. The *printf* function in line eight uses two statements: a string and an integer variable. The string is an immediate value. Change the name "James" to your own name, unless your name is also James.

You don’t need to guess how many months you have because that value is calculated as the argument in the *printf* function at line nine. Save the code, build and run. Of course, the month’s value displayed is an approximation, unless today is your birthday. In that case, Happy Birthday!

The *int* is really one variable type. Another common type is the char or character variable. Take a look at the code below:

```c
1 #include <stdio.h>
2
3 int main()
```

Here, three character variables are declared: `x`, `y`, and `z`. You can declare multiple variables of the same type on a single line, as long as each variable name is separated by a comma. Lines 7-9 assign the variables characters—single quotes are used. Then the values are displayed by the *printf* function at line 11. Save, build, and run the code.

Just as you can change integer variables, you can also change character variables. You can even do math. Edit line eight to read:

```c
1 #include <stdio.h>
2
3 int main()
4 {
5 char x, y, z;
6
7 x = 'A';
8 y = x+1;
9 z = 'C';
10
11 printf("It's as easy as %c%c%c\n", x,y,z);
12
13 return(0);
14 }
15
```

Then, edit line nine to read:

```c
1 #include <stdio.h>
2
3 int main()
4 {
5 char x, y, z;
6
7 x = 'A';
```

The terms "Interoperability" and "Coexistence" are sometimes used in place of migration but are different concepts:

Interoperability is the ability of two systems to understand each other and, therefore, be able to exchange information. For example, two different e-mail servers may be able to exchange mail messages thanks to Simple Mail Transfer Protocol (SMTP).

Coexistence is the ability of two systems to operate on the same resource. For example, two different file systems can both be installed on the same computer, but they cannot read each other's files. A system that can read from or write to both file systems provides a migration path.

A migration strategy should consider:

- Data Migration
- Application Migration
- User Migration

![](img/7d7500a0ed1507e3351945dfe5a0440d_60_0.png)

Migration should not be confused with new development. And other concepts and principles should also be considered in a migration roadmap:

- Keep it simple
- Methodology
- Simplicity, Openness, Scalability (SOS)

Note: The figure shows a flow from Legacy Infrastructure to Target Infrastructure via a Migration Factory.

placeholder is used to represent floating point values in a *printf* statement. Build and run the code.

The value generated for pi is accurate down to the hundreds place, which is okay for quite a few things in antiquity, but not acceptable for modern calculations.

## Chapter 5: Character I/O Functions in C

Programs are both known for input and output. Output goes to the standard output device, which is usually the screen or terminal window. Input comes from the standard input device, which is normally the keyboard. In this chapter, we'll explore input and output concepts in C. These involve character I/O, which is the reading of single characters, as well as the output of a single character. We'll also touch upon the concept of stream input and output.

The two most common C language character I/O functions are *getchar()* and *putchar()*. *getchar()* fetches the standard input. *putchar()* sends a character to standard output. Both of these functions require the inclusion of the stdio.h header file for their prototypes and such.

Although they are character functions, they work with integer values. Yes, that's weird, but so are many things in the C language. In fact, you may find yourself frequently using *char* variables with these functions. When you do, the compiler may gently warn you about the mistake. Finally, these functions are stream oriented, which is something we'll discuss in the later chapters.

Take a look at the code below:

```c
1 #include <stdio.h>
2
3 int main()
4 {
5 int c;
6
7 printf("Type a letter: ");
8 c = getchar();
9 printf("You typed '%c':\n", c);
10
11 return(0);
12 }
13
```

Integer variable `c` is declared at line 5. It is used with the *getchar()* function at line eight, storing a single character from the input stream. In this example, that would be a character typed at the keyboard. The character is displayed at line nine. The int variable `c` is used, but the character placeholder %c is specified. This ensures that the character is displayed, not its code value. Build and run the code.

Note that the prompt in the output keeps the cursor at the same line, and we've added a space to make it more readable. Type a letter, such as a big letter 'Z', and press the Enter key. As you can see in the output, it will immediately specify the letter that you typed.

Now, modify the code so that the *putchar()* function outputs the character you typed. To do that, you need to split the *printf* function in two, like so:

```c
1 #include <stdio.h>
2
3 int main()
4 {
5 int c;
printf("Type a letter: ");
c = getchar();
printf("You typed '");
putchar(c);
printf("'.\n");
return(0);
}
```

Edit it to where it says, "You typed" and notice how we kept that single quote after that string. Close the string in parenthesis and end the statement with a semicolon. Then add *putchar()* on line ten, and then display the rest of the string by using `printf()`. The argument `c` is no longer needed. Instead, it appears in line ten with the *putchar()* function where it is output directly. Save, build and run the source code file.

The solution provides for the putchar() function to generate output. But it also makes the code longer and less readable. That is actually okay in C, and you’ll discover that the output is unchanged. Save, build and run the code.

You can also use the putchar() function with immediate values. At this point in the code, the statement at line 11 really just outputs three characters: the single quote, period, and the new line. We could change line 11 to read:

```c
1 #include <stdio.h>
2
3 int main()
4 {
5 int c;
6
7 printf("Type a letter: ");
8 c = getchar();
9 printf("You typed ");
10 putchar(c);
11 putchar('\'');
12 printf(".\n");
13
14 return(0);
15 }
16
```

At line 11, type a single quote, a backslash, a single quote, and then another single quote. That looks odd, but you have to escape the single quote character. Otherwise, the compiler becomes confused. A second putchar() function would display the period. The final putchar() function would display the escape sequence, which is specified in the original printf function as a new line.

```c
1 #include <stdio.h>
2
3 int main()
4 {
```
