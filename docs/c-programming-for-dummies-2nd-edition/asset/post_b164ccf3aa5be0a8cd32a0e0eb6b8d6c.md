
- The B programming language, upon which C is based, was named after the B in Bell Labs.
- BCPL stands for Basic Combined Programming Language.
- The C++ programming language is quite similar to C, but it's not merely an extension or an add-on. It's easier to learn C++ when you know C, but it's not easy to switch between the languages.
- A D programming language exists. Developed in the early 2000s, it's not as popular today as other current languages, such as Python and Java.
- Unfortunately, I have no idea how to pronounce "Bjarne Stroustrup."

## The Programming Process

No matter which language you use, certain procedures are common to the programming process. In this manner, learning to program is like learning to cook: You must take things in a certain order, whether the result is crème brûlée or a smoldering pile of egg glop.

### Understanding programming

The goal of programming is to create a program. The language is C, and the tools are the editor, compiler, and linker — or an IDE, which combines everything. The result is a program that directs the hardware to do something. That hardware can be a computer, tablet, phone, microcontroller, or whatever.

Step-by-step, the programming process works like this:

1. Write the source code.
2. Compile and link, or build, the source code into a program.
3. Run and test the program.

A human (you) writes source code. The source code is built into a program in two steps: compiling it into object code and then linking the object code with C libraries to build the program. Finally, that program is run.

The reality goes more like this:

1. Write the source code.
2. Compile the source code into object code.
3. Fix warnings and repeat Steps 1 and 2.
4. Link the object code with libraries to build the program.
5. Fix errors and repeat Steps 1 through 4.
6. Run and test the program.
7. Fix bugs by repeating the entire process.

Or, more frequently, the program runs fine but you want to add a feature or refine an element. Then you repeat everything.

Hopefully, Steps 3, 5, and 7 don't happen often. Still, you do a lot of fixing in the programming cycle.

The good news is that the compiler dutifully reports the errors and even shows you where they are. That's better than tracking down a bug in miles of wires back in the old ENIAC days.

> - Despite having "build" as a single step, the compiler still creates object code, and a linker links the object code into a program. If you goof up royally, linking doesn't even happen and you must fix the compiler warnings before taking the next step.
> - One of my professional programmer friends said that the art form should be called debugging, not programming.
> - Legend has it that the first computer bug was a moth that Grace Hopper found in the wiring of an early computer. There's some doubt about this legend, considering that the word *bug* has been used since Shakespeare's time to describe something quirky or odd.

![](img/dcc0cd79d4a45cfce24fa49d85442884_39_0.png)

### Writing source code

*Source code* represents the part of the process that contains the programming language itself. You use a text editor to write a source code file.

In this book, source code is shown in program listings, such as the example in Listing 2-1.

**LISTING 2-1: Standard "Hello World" Program**

```c
#include <stdio.h>

int main()
{
    puts("Greetings, human.");
    return 0;
}
```

Line numbers are not shown in this book's listings. They aren't part of the code, and showing them here can be confusing. The text editor may display line numbers for reference purposes.

In this book, you're directed to type the source code from a listing as part of an exercise. For example:

**Exercise 2-1:** Start a new project in Code::Blocks named ex0201. Or use your text editor to create the source code file ex0201.c for compiling and linking at the command prompt.

Do it: Obey Exercise 2-1, either in Code::Blocks, at the command prompt in a terminal window, or in another C language IDE, such as Xcode on the Mac.

1. **Write the source code in the editor, copying it from Listing 2-1.**
   
   Alternatively, you can copy-and-paste the code from the companion website or use the listing's source code file, downloaded from the website. Refer to this book's introduction for details.
   
   If you're creating a Code::Blocks project, erase the skeleton that's provided and replace it with the code shown in Listing 2-1.
2. **Save the source code file.**

There. You've just completed the first step in the programming process — writing source code. The next section continues your journey with the compiler.

![](img/dcc0cd79d4a45cfce24fa49d85442884_40_0.png)

- All C source code files end with the .c ("dot-see") filename extension.
- In Windows, I recommend that you set the folder display options so that filename extensions appear.
- C++ source code files have the extension .cpp ("dot-see-pee-pee"). I shall refrain from writing a puerile joke here.

> Source code files follow the same naming conventions as any file on a computer. Traditionally, a small program has the same name (but not extension) as the final program. If your program is named puzzle, the source code is most likely named puzzle.c.

### Compiling and linking

Traditionally, the compiler reads text from a source code file and translates that text — a programming language — into something called object code. The linker then creates the final program. It links the object code file with C language libraries to create a program. All this happens exactly as written — unless a warning or an error crops up along the way.

You can compile and link separately in an IDE or at the command prompt. Fortunately, modern compilers combine both steps in a process called build.

![](img/dcc0cd79d4a45cfce24fa49d85442884_41_0.png)

To build the project for Listing 2-1 in Code::Blocks, click the Build toolbar button (shown in the margin) or choose Build > Build from the menu. Any errors present themselves on the Build Log tab as well as on the Build Messages tab.

```
clang -c -Wall ex0201.c
```

First comes the compiler name, clang, followed by the -Wall switch to report all warnings. The final argument is the source code filename. Upon success, you see no feedback; otherwise, warnings and error messages spill on the screen like fruit from an upturned apple cart.

(Running the program file is covered in the next section.)

> The object code file has the same name as the source code file, but ends in .o ("dot-o"). If the source code file is named ex0201.c the object code file is named ex0201.o. The modern build process deletes this file unless you specifically direct the compiler to generate and retain the object code file.

As the compiler translates your C code into object code, it checks for common mistakes, missing items, and other issues. If anything is awry, the compiler displays a list of warnings. To fix them, you re-edit the source code and attempt to compile once again.

The linker brings in the C language library, which is how the final program is built. The libraries contain the actual instructions that tell the computer (or whatever device) what to do. Those instructions are executed based on the shorthand directions found in the object code.

Any mistakes found by the linker are called errors. When errors occur, a program isn't created; errors are fatal.

Some C programs link in several libraries, depending on what the program does. In addition to the standard C library, you can link libraries for working with graphics, networking, sound, and so on. As you learn more about programming, you'll discover how to choose and link in various libraries. Chapter 24 offers the details.

### Running and testing

The next thing to do after building is to run the result. Running is necessary, primarily to demonstrate that the program does what you intend and in the manner you desire.

When the program doesn't work, you must go back and fix the source code and try again. Yes, it's entirely possible to build a program and see no warnings or errors and then find that the thing doesn't work. It happens all the time.

Continue with Exercise 2-1: Run the program.

In Code::Blocks, choose Build > Run or click the Run toolbar button, shown in the margin.

At the command prompt, type the program name prefixed by the current directory:

```
./a.out
```

## PREPROCESSOR DIRECTIVES

Beyond source code, a C compiler also deals with special instructions called preprocessor directives. For example, Listing 2-1 shows the following preprocessor directive:

```c
#include <stdio.h>
```

The include directive instructs the compiler to locate the header file stdio.h. The contents of this file are inserted into the source code at compile time. Together, both files are converted into object code.
