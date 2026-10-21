
## Class Inheritance and Virtual Functions

1. What's wrong with the following code?

```
class CBadClass
{
private:
    int len;
    char* p;
public:
    CBadClass(const char* str): p(str), len(strlen(p)) {}
    CBadClass() {}
};
```

2. Suppose you have a class CBird, as follows, that you want to use as a base class for deriving a hierarchy of bird classes:

```
class CBird
{
protected:
    int wingSpan;
    int eggSize;
    int airSpeed;
    int altitude;
public:
    virtual void fly() { altitude = 100; }
};
```

Is it reasonable to create a CHawk by deriving from CBird? How about a COstrich? Justify your answers. Derive an avian hierarchy that can cope with both of these birds.

3. Given the following class:

```
class CBase
{
protected:
    int m_anInt;
public:
    CBase(int n) : m_anInt(n) { cout << "Base constructor\n"; }
    virtual void Print() const = 0;
};
```

What sort of class is CBase and why? Derive a class from CBase which sets its inherited integer value, m_anInt, when constructed, and prints it on request. Write a test program to verify that your class is correct.

4. A binary tree is a structure made up of nodes where each node contains a pointer to a “left” node and a pointer to a “right” node plus a data item, as shown in Figure 9-7. The tree starts with a root node, and this is the starting point for accessing the nodes in the tree. Either or both pointers in a node can be null. Figure 9-7 shows an ordered binary tree, which is a tree organized so that the value of each node is always greater than or equal to the value of the left node and less than or equal to the value of the right node. Define a native C++ class to define an ordered binary tree that stores integer values. You also need to define a Node class, but that can be an inner class to the BinaryTree class. Write a program to test the operation of your BinaryTree class by storing an arbitrary sequence of integers in it and retrieving and outputting them in ascending sequence. Hint: Don’t be afraid to use recursion.

![](img/2359b0c604600c58fba3539c738a356e_605_0.png)

## An Ordered Binary Tree

Figure 9-7

5. Implement Exercise 4 as a CLR program. If you did not manage to complete Exercise 4, look at the solution in the download and use that as a guide to doing this exercise.

6. Define a generic BinaryTree class for any type that implements the IComparable interface class and demonstrate its operation by using instances of the generic class to store and retrieve first a number of random integers, and then the elements of the following array:

```
array<String^>^ words = {L"Success", L"is", L"the", L"ability", L"to",
L"go" , L"from", L"one", L"failure", L"to",
L"another", L"with", L"no", L"loss", L"of",
L"enthusiasm"};
```

7. Write the values retrieved from the binary tree to the command line.

## Debugging Techniques

If you have been doing the exercises in the previous chapters, you have most likely been battling with bugs in your code. In this chapter you will explore how the basic debugging capabilities built into Visual C++ 2005 can help with this. You will also investigate some additional tools that you can use to find and eliminate errors from your programs, and see some of the ways in which you can equip your programs with specific code to check for errors.

In this chapter, you will learn about:

- How to run your program under the control of the Visual C++ 2005 debugger
- How to step through your program a statement at a time
- How to monitor or change the values of variables in your programs
- How to monitor the value of an expression in your program
- The call stack
- Assertions and how to use them to check your code
- How to add debugging specific code to a program
- How to detect memory leaks in a native C++ program
- How to use the execution tracing facilities and generate debugging output in C++/CLI programs

Bugs are errors in your program and debugging is the process of finding and eliminating them. You are undoubtedly aware by now that debugging is an integral part of the programming process — it goes with the territory as they say. The facts about bugs in your programs are rather depressing:

## Chapter 10

- Every program you write that is more than trivial will contain bugs that you need to try to expose, find, and eliminate if your program is to be reliable and effective. Note the three phases here—a program bug is not necessarily apparent; even when it is apparent you may not know where it is in your source code; and even when you know roughly where it is, it may not be easy to determine what exactly is causing the problem and thus eliminate it.
- Many programs that you write will contain bugs even after you think you have fully tested them.
- Program bugs can remain hidden in a program that is apparently operating correctly—sometimes for years. They generally become apparent at the most inconvenient moment.
- Programs beyond a certain size and complexity always contain bugs, no matter how much time and effort you expend testing them. (The measure of size and complexity that guarantees the presence of bugs is not precisely defined, but Visual C++ 2005 and your operating system certainly come into this category.)

It is unwise to dwell on this last point if you are of a nervous disposition, especially if you fly a lot or regularly are in the vicinity of any process dependent on computers for proper operation can be damaging to your health in the event of failure.

Many potential bugs are eliminated during the compile and link phases, but there are still quite a few left even after you manage to produce an executable module for your program. Unfortunately, despite the fact that program bugs are as inevitable as death and taxes, debugging is not an exact science; however, you can still adopt a structured approach to eliminating bugs. There are four broad strategies you can adopt to make debugging as painless as possible:

- Don’t re-invent the wheel. Understand and use the library facilities provided as part of Visual C++ 2005 (or other commercial software components you have access to) so that your program uses as much pre-tested code as possible.
- Develop and test your code incrementally. By testing each significant class and function individually, and gradually assembling separate code components after testing them, you can make the development process much easier, with fewer obscure bugs occurring along the way.
- Code defensively—which means writing code to guard against potential errors. For example, declare member functions of native C++ classes that don’t modify an object as const. Use const parameters where appropriate. Don’t use ‘magic numbers’ in your code—define const objects with the required values.
- Include debugging code that checks and validates data and conditions in your program from the outset. This is something you will look at in detail later in this chapter.

Because of the importance of ending up with programs that are as bug-free as is humanly possible, Visual C++ 2005 provides you with a powerful armory of tools for finding bugs. Before you get into the detailed mechanics, however, look a little closer at how bugs arise.

## Program Bugs

Of course, the primary originator of bugs in your program is you and the mistakes you make. These mistakes range from simple typos — just pressing the wrong key — to getting the logic completely wrong. I, too, find it hard to believe that I can make such silly mistakes so often, but no one has yet managed to come up with a credible alternative as to how bugs get into your code — so it must be true! Humans are creatures of habit so you will probably find yourself making some mistakes time and time again. Frustratingly, many errors are glaringly obvious to others, but invisible to you — this is just your computer’s way of teaching you a bit of humility. Broadly there are two kinds of errors you can make in your code that result in program bugs:

- Syntactic errors — These are errors that you result from statements that are not of the correct form; for example, if you miss a semicolon from the end of a statement or use a colon where you should put a comma. You don’t have to worry too much about syntactic errors. The compiler recognizes all syntactic errors, and you generally get a fairly good indication of what the error is so it’s easy to fix.

- Semantic errors — These are errors where the code is syntactically correct, but it does not do what you intended. The compiler cannot know what you intended to achieve with your program, so it cannot detect semantic errors; however, you will often get an indication that something is wrong because the program terminates abnormally. The debugging facilities in Visual C++ 2005 are aimed at helping you find semantic errors. Semantic errors can be very subtle and difficult to find, for example, where the program occasionally produces the wrong results or crashes infrequently. Perhaps the most difficult of such bugs arise in multi-threaded programs where concurrent paths of execution are not managed properly.

Of course, there are bugs in the system environment that you are using (Visual C++ 2005 included) but this should be the last place you suspect when your program doesn’t work. Even when you do conclude that it must be the compiler or the operating system, nine times out of ten you will be wrong. There are certainly bugs in Visual C++ 2005, however, and if you want to keep up with those identified to date, together with any fixes available, you can search the information provided on the Microsoft web site related to Visual C++ (http://msdn.microsoft.com/visualc/), or better still, if you can afford a subscription to Microsoft Developer Network, you get quarterly updates on the latest bugs and fixes.

It can be helpful to maker a checklist of bugs you find in your code for future reference. By examining new code that you write for the kinds of errors you have made in the past, you can often reduce the time needed to debug new projects.

From the nature of programming, bugs are virtually infinite in their variety, but there are some kinds that are particularly common. You may be well aware of most of these, but take a quick look at them anyway.

## Common Bugs

A useful way of cataloguing bugs is to relate them to the symptoms they cause because this is how you experience them in the first instance. The following list of five common symptoms is by no means exhaustive, and you are certainly able to add to it as you gain programming experience:
