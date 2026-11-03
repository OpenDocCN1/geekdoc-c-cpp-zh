
## Operators

Mixed in with functions and keywords are various symbols collectively known as operators. Most of them are mathematic in origin, including traditional symbols like the plus (+), minus (−), and equal (=) signs.

Operators get thrown in with functions, keywords, and other parts of the C language; for example:

```
result = sqrt(value) + 5;
```

Here, the = and + operators are used to concoct some sort of mathematical mumbo jumbo.

Not all C language operators perform math. Appendix C lists the lot.

![](img/dcc0cd79d4a45cfce24fa49d85442884_48_0.png)

## Variables and values

A program works by manipulating information stored in variables. A variable is a container into which you can stuff values, characters, or other forms of information. The program can also work on specific, unchanging values that I call immediate values:

```
result = sqrt(value) + 5;
```

In this example, result and value are variables; their content is unknown by looking at the code, and the content can change as the program runs. The number 5 is an immediate value.

C sports different types of variables, each designed to hold specific values or data types. Chapter 6 explains variables and values in more detail.

## Statements and structure

As with human languages, programming languages feature syntax — it’s the method by which the pieces fit together. Unlike English, where syntax can be determined by rolling dice, the method by which C puts together keywords, functions, operators, variables, and values is quite strict.

The core of the C language is the statement, which is similar to a sentence in English. A statement is an action, a direction that the program gives to the hardware. All statements end with a semicolon, the C language equivalent of a period:

```
beep();
```

Here, the single function beep() is a statement. It can be that simple. In fact, a single semicolon on a line can be a statement:

```
;
```

The preceding statement does nothing.

Statements in C are executed one after the other, beginning at the top of the source code and working down to the bottom. Ways exist to change that order as the program runs, which are presented elsewhere in this book.

The paragraph-level syntax for the C language involves blocks. These are defined by enclosing statements in a pair of curly brackets, or braces:

```
{
    if( money < 0 ) get_job();
    party();
    sleep(24);
}
```

These three statements form a block, held within curly brackets, indicating that they belong together. They're either part of a function or part of a loop or something similar. Regardless, they all go together and are executed one after the other.

You'll notice that the statements held within a block are indented one tab stop. That's a tradition in C, but it's not required. The term whitespace is used to refer to tabs, empty lines, and other empty parts of the source code.

Generally, the C compiler ignores whitespace, looking instead for semicolons and curly brackets. For example, you can edit the source code from Listing 2-1 to read:

```
#include <stdio.h>
int main(){puts("Greetings, human.");return 0;}
```

That's two lines of source code where before you saw several. The include directive must be on a line by itself, but the C code can be all scrunched up with no whitespace. The code compiles successfully.

Thankfully, most programmers use whitespace to make their code more readable.

![](img/dcc0cd79d4a45cfce24fa49d85442884_50_0.png)

> A common mistake made by beginning C language programmers is forgetting to place the semicolon after a statement. It's also a common mistake made by experienced programmers!
>
> The compiler is the tool that finds missing semicolons. That's because when you forget the semicolon, the compiler assumes that two statements are really one statement. The effect is that the compiler becomes confused and, therefore, in a fit of panic, flags those lines of source code with a warning or error.

## Comments

Some items in your C language source code are parts of neither the language nor the structure. Those are comments, which can be information about the program, notes to yourself, or filthy limericks.

Traditional C comments begin with the /* characters and end with the */ characters. All text between these two markers is ignored by the compiler, shunned by the linker, and avoided in the final program.

Listing 3-1 shows an update to the code from project ex0201, where comments have been liberally added.

### LISTING 3-1: Overly Commented Source Code

```c
/* Author: Dan Gookin */
/* This program displays text on the screen */

#include <stdio.h>  /* Required for puts() */

int main()
{
    puts("Greetings, human.");  /* Displays text */
    return 0;
}
```

Comments in Listing 3-1 appear on a line by itself or at the end of a line. The first two lines can be combined for a multiline comment, as shown in Listing 3-2.

### LISTING 3-2: Multiline Comments

```c
/* Author: Dan Gookin
   This program displays text on the screen */

#include <stdio.h>    /* Required for puts() */

int main()
{
    puts("Greetings, human.");  /* Displays text */
    return 0;
}
```

All text between the `/*` and the `*/` is ignored. Some source code editors, such as the one in Code::Blocks, display commented text in a unique color, which further confirms how the compiler sees and ignores the comment text. If you like, type the source code from Listing 3-2 into a text editor to see how comments work and whether they're highlighted.

A second comment style uses the double-slash (`//`) characters, which originated in the C++ language but is also available in C. This type of comment affects text on one line, from the `//` characters to the end of the line, as shown in Listing 3-3.

### LISTING 3-3: Double-Slash Comments

```c
#include <stdio.h>

int main()
{
    puts("Greetings, human.");  // Displays text
    return 0;
}
```

Don't worry about putting comments in your text at this point, unless you're at a university somewhere and the professor is ridiculously strict about it. Comments are for you, the programmer, to help you understand your code and remember what your intentions are. They come in handy down the road, when you're looking at your code and not fully understanding what you were doing. This situation happens frequently.

## Behold the Typical C Program

All C programs feature a basic structure, which is easily shown by looking at the C source code skeleton that Code::Blocks uses to start a new project, as shown in Listing 3-4.

### LISTING 3-4: Code::Blocks C Skeleton

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    printf("Hello world!\n");
    return 0;
}
```

This listing isn't the bare minimum, but it gives a rough idea of the basic C program.

![](img/dcc0cd79d4a45cfce24fa49d85442884_52_0.png)

> Just as you read text on a page, C source code flows from the top down. The program starts execution at the first line, and then the next line, and so on until the end of the source code file. Exceptions to this order include decision-making structures and loops, but mostly the code runs from the top down.
>
> Decision-making structures are covered in Chapter 8; loops are introduced in Chapter 9.

### Understanding C program structure

To better understand how C programs come into being, you can create the simplest, most useless type of C program.

**Exercise 3-1:** Follow the steps in this section to create a new source code file, named ex0301.c. You can use Code::Blocks to create a new project or use a text editor and build the project in a terminal window at the command prompt.

Here are the specific steps:

- **1. Edit the source code to match Listing 3-5.**  
  That's not a misprint. The source code is blank, empty. If you're using Code::Blocks, erase the skeleton provided.
- **2. Save the source code.**
- **3. Build.**  
  Nothing happens or you see a linker error message.

### LISTING 3-5: A Simple Program That Does Nothing

Because the source code is empty, no object code is generated. Even if a program is created, it's empty and does nothing. That's what you told the compiler to do, and the resulting program did it well.

### Setting the main() function

All C programs have a main() function. It's the first function that's run when a program starts. As a function, it requires parentheses for its arguments but also curly brackets to hold the function's statements in a block, as shown in Listing 3-6.

**Continue with Exercise 3-1:** Rebuild the source code `ex0301.c`, as shown in Listing 3-6. Save the project. Build and run.

### LISTING 3-6: The main() Function

```
main() {}
```

You may see a warning because the main() function lacks a data type. That's okay. Otherwise, the program generates no output — which is great! You didn't direct the code to do anything, and it did it well. What you see is the minimum C program. It's also known as the dummy program.
