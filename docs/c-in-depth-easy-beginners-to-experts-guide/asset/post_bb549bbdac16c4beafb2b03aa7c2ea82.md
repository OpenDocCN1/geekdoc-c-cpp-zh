
data type to represent normal variables that hold different entities, then we will soon lose track of what the integer values actually represent; this is handled by use of typedefs, okay!!

## (B)

In Windows programming at several places we are required to gather and work with dissimilar but inter-related data. This can be done using a structure.

## Some Notes

- Use a 32-bit compiler for Windows programming like Visual C++.
- Use the header file windows.h.

## Our First “C” Under Windows Programming

### 150. Write a Program That Prints “Hello!”

```c
#include <windows.h>

int _stdcall WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance,
                     LPSTR pszCmdLine, int nCmdShow)
{
    MessageBox(0, "Hello!", "Title", 0);
    return(0);
}
```

## Heavy Mind Wash Drill Notes

### 1.

Always use a 32-bit compiler for 32-bit operating system development like Microsoft Visual C++, or for 64-bit operating system development use a 64-bit compiler, okay!!

### 2.

I want to tell you that every DOS program’s execution begins with the main() function; on the other hand, every Windows program begins its execution with the WinMain() function, as you saw before.

### 3.

_stdcall is used before WinMain()—it shows the calling conventions used by the WinMain() function. Calling conventions indicate two things:

- (a) The order (left to right or right to left) in which the arguments are pushed onto the stack when a function call is made.
- (b) The caller function or called function removes the arguments from the stack at the end of the call. There are many calling conventions available like _cdecl and _stdcall; both of these calling conventions pass arguments from right to left. All API functions use _stdcall; if not mentioned, then the compiler assumes _cdecl conventions, okay!!

### 4.

HINSTANCE and LPSTR are nothing but typedefs. The first is an unsigned int and the second is a pointer to a char. These typedefs are defined in ‘windows.h’. This header file always contains these typedefs while writing any “C” under Windows program.

### 5.

hInstance, hPrevInstance, lpszCmdLine and nCmdShow are variable names; you can also use variable names like i, j, k or any others in place of them.

![](img/3a2b6e5e90a58a56458b0539952c0cd2_403_0.png)

## Explanation of Whole Program

### WinMain() Receives Four Parameters, Which Are as Follows

### hInstance

This is an “instance handle” for the running application. Windows creates this ID number when the application starts. We will use this value in many Windows functions to identify application data. And the most important thing: a handle is simply a 32-bit number that refers to an entity; the entity may be a cursor, a brush, an icon, a file, a device, or anything, okay!!

### hPrevInstance

This parameter is a remnant of earlier versions of Windows; now it is no longer used, hence its value contains 0. This shows only backward compatibility.

### lpszCmdLine

This is a pointer to a character string containing the command-line arguments passed to the program. This is similar to the argv, argc parameters passed to main(), just like in a DOS program.

### nCmdShow

This is an integer value that is passed to the function. This integer tells the program how the window should appear when it is displayed for the first time.

### MessageBox() Function

This function pops up a message box whose title is “Title” and which contains a message “Hello!”

*Returning 0 from WinMain() indicates success; a non-zero value shows failure.*

![](img/3a2b6e5e90a58a56458b0539952c0cd2_404_0.png)

# Chapter ∞ 21—Part II ∞ (Programming Guidelines)

This chapter explains how to write computer programs that work and that are understandable to other intelligent beings! These two attributes are not independent! In general, programs that other programmers cannot understand do not work very well. (Not to mention the fact that they are maintenance nightmares!)

Writing structured programs (structured code and data!) helps greatly in debugging the code. Here is a quick review of some of the features of a structured program.

- 1. Lots of well-defined functions!
- 2. Using structured loop constructs (i.e., while and for) instead of goto.
- 3. Using variables that have one purpose and meaningful names.
- 4. Using structured data types to represent complex data.
- 5. Using the ADT (Abstract Data Type) or OOP (Object-Oriented Programming) paradigm of programming.

The most common types of mistakes when programming are:

- 1. Programming without thinking.
- 2. Writing code in an unstructured manner.

Let’s take these in order.

## 1.1 Thinking About Programming

When a real programmer (or programming team) is given a problem to solve, they do not immediately sit down at a terminal and start typing in code! They first design the program by thinking about the numerous ways the problem’s solution may be found.

One of the biggest myths of programming is that: “The sooner I start coding the sooner a working program will be produced.” This is NOT true!! A program that is planned before coding will become a working program before an unplanned program.

Yes, an unplanned program will be typed in and maybe compiled faster, but these are just the first steps of creating a working program! Next comes the debugging stage.

This is where the benefits of a planned program will appear. In the vast majority of the time, a planned program will have fewer bugs than an unplanned program. In addition, planned programs are generally more structured than unplanned programs. Thus, finding the bugs will be easier in the planned program.

So how does one design a program before coding? There are several different techniques. One of the most common is called top-down design. Here an outline of the program is first created. (Essentially, one first looks at the general form of the main() function and then recursively works down to the lowest level functions.) There are many references on how to write programs in this manner.

Top-down design divides the program into sub-tasks. Each sub-task is a smaller problem that must be solved. Problems are solved by using an algorithm.

Functions (and data) in the program implement the algorithm. Before writing the actual code, take a very small problem and trace by hand how the chosen algorithm would solve it.

This serves several purposes:

- 1. It checks out the algorithm to see if it will actually work on the given problem. (If it does not work, you can immediately start looking for another algorithm. Note that if you had immediately started coding, you would probably not discover the algorithm would not work until many lines of code had been entered!)
- 2. Makes sure that you understand how the algorithm actually works! (If you cannot trace the algorithm by hand, you will not be able to write a program to do it!)
- 3. Gives you the detailed workings of a short, simple run of the algorithm that can be used later when debugging the code.

Only when you are confident that you understand how the entire program will look in code.

## 1.2 Structured Programming

When a program is structured, it is divided into sub-units that may be tested separately. This is a great advantage when debugging! Code in a sub-unit may be debugged separately from the rest of the program code. I find it useful to debug each sub-unit as it is written. If no debugging is performed until the entire program is written, debugging is much harder.

The entire source of the program must be searched for bugs. If sub-units are debugged separately, the source code that must be searched for bugs is much smaller! Storing the sub-units of a program into separate source files can make it easier to debug them separately.

The ADT and OOP paradigms also divide programs into sub-units. Often with these methods, the sub-units are even more independent than with normal structured code. This has two main advantages:

- 1. Sub-units are even easier to debug separately.
- 2. Sub-units can often be reused in other programs. (Thus, a new program can use a previously debugged sub-unit from an earlier program)

Sub-units are generally debugged separately by writing a small driver program. Driver programs set up data for the sub-task that the sub-unit is supposed to solve, call the sub-unit to perform its sub-task, and then display the results so that they can be checked.

Of course, all the following debugging methods can be used to debug a sub-unit, just as they can be used to debug the entire program. Again, the advantages of sub-units are that they are only part of the program and so are easier to debug than the entire program at once!

## 2. Compiling Programs
