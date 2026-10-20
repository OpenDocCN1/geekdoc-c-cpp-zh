
## Exercises

21.3 (Explain Notation) Explain the use of the following notation in a Java program:

```
public class Array< T > { }
```

21.4 (Generic Method selectionSort) Write a generic method selectionSort based on the sort program of Figs. 19.6–19.7. Write a test program that inputs, sorts and outputs an Integer array and a Float array. [Hint: Use <T extends Comparable<T> > in the type-parameter section for method selectionSort, so that you can use method compareTo to compare the objects of the type that T represents.]

21.5 (Overloaded Generic Method printArray) Overload generic method printArray of Fig. 21.3 so that it takes two additional integer arguments, lowSubscript and highSubscript. A call to this method prints only the designated portion of the array. Validate lowSubscript and highSubscript. If either is out of range, the overloaded printArray method should throw an InvalidSubscriptException; otherwise, printArray should return the number of elements printed. Then modify main to exercise both versions of printArray on arrays integerArray, doubleArray and characterArray. Test all capabilities of both versions of printArray.

21.6 (Overloading a Generic Method with a Nongeneric Method) Overload generic method printArray of Fig. 21.3 with a nongeneric version that specifically prints an array of Strings in neat, tabular format, as shown in the sample output that follows:

```
Array stringArray contains:
one    two    three    four
five   six    seven    eight
```

21.7 (Generic isEqualTo Method) Write a simple generic version of method isEqualTo that compares its two arguments with the equals method and returns true if they’re equal and false otherwise. Use this generic method in a program that calls isEqualTo with a variety of built-in types, such as Object or Integer. What result do you get when you attempt to run this program?

21.8 (Generic Class Pair) Write a generic class Pair which has two type parameters—F and S—each representing the type of the first and second element of the pair, respectively. Add get and set methods for the first and second elements of the pair. [Hint: The class header should be public class Pair<F, S>.]

21.9 (Overloading Generic Methods) How can generic methods be overloaded?

21.10 (Overload Resolution) The compiler performs a matching process to determine which method to call when a method is invoked. Under what circumstances does an attempt to make a match result in a compile-time error?

21.11 (What Does this Statement Do?) Explain why a Java program might use the statement

```
ArrayList< Employee > workerList = new ArrayList< Employee >();
```

## 22

## Custom Generic Data Structures

> Much that I bound, I could not free;
> Much that I freed returned to me.
> —Lee Wilson Dodd

> ‘Will you walk a little faster?’ said a whiting to a snail,
> ‘There’s a porpoise close behind us, and he’s treading on my tail.’
> —Lewis Carroll

> There is always room at the top.
> —Daniel Webster

> Push on—keep moving.
> —Thomas Morton

> I’ll turn over a new leaf.
> —Miguel de Cervantes

## Objectives

In this chapter you’ll learn:

- To form linked data structures using references, self-referential classes, recursion and generics.
- To create and manipulate dynamic data structures, such as linked lists, queues, stacks and binary trees.
- Various important applications of linked data structures.
- How to create reusable data structures with classes, inheritance and composition.

![](img/009e962758dcc71dbc43a493362e6dc0_941_0.png)

## 22.1 Introduction

This chapter shows how to build dynamic data structures that grow and shrink at execution time. Linked lists are collections of data items “linked up in a chain”; insertions and deletions can be made anywhere in a linked list. Stacks are important in compilers and operating systems; insertions and deletions are made only at one end of a stack—its top. Queues represent waiting lines; insertions are made at the back (also referred to as the tail) of a queue and deletions are made from the front (also referred to as the head). Binary trees facilitate high-speed searching and sorting of data, eliminating duplicate data items efficiently, representing file-system directories, compiling expressions into machine language and many other interesting applications.

We discuss each of these major data-structure types and implement programs that create and manipulate them. We use classes, inheritance and composition to create and package them for reusability and maintainability. In general, you’d use one of the pre-defined collection classes that we discussed in Chapter 20. However, the techniques we present here can be used if you ever need to build your own custom collections.

For simplicity, this chapter’s examples manipulate primitive values. However, the data-structure implementations we develop here can store objects of most types.

If you feel ambitious, you might want to attempt the major project described in the special section entitled Building Your Own Compiler, which we’ve posted online at www.deitel.com/books/jhtp9/. You’ve been using a Java compiler to translate your Java programs to bytecodes so that you could execute these programs. In this project, you’ll actually build your own compiler. It will read statements written in a simple, yet powerful high-level language similar to early versions of the popular language BASIC and translate these statements into Simpletron Machine Language (SML) instructions—SML is the language you learned in the Chapter 7 special section, Building Your Own Computer. Your Simpletron Simulator program will then execute the SML program produced by your compiler! Implementing this project by using an object-oriented approach will give you an opportunity to exercise most of what you’ve learned in this book. The special section carefully walks you through the specifications of the high-level language and describes the algorithms you’ll need to convert each high-level language statement into machine-language instructions. If you enjoy being challenged, you might attempt the enhancements to both the compiler and the Simpletron Simulator suggested in the exercises.

## 22.2 Self-Referential Classes

A self-referential class contains an instance variable that refers to another object of the same class type. For example, the generic Node class declaration

- 22.1 Introduction
- 22.2 Self-Referential Classes
- 22.3 Dynamic Memory Allocation
- 22.4 Linked Lists
- 22.5 Stacks
- 22.6 Queues
- 22.7 Trees
- 22.8 Wrap-Up

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Special Section: Building Your Own Compiler

```
class Node< T >
{
    private T data;
    private Node< T > nextNode; // reference to next linked node
    public Node( T data ) { /* constructor body */ }
    public void setData( T data ) { /* method body */ }
    public T getData() { /* method body */ }
    public void setNext( Node< T > next ) { /* method body */ }
    public Node< T > getNext() { /* method body */ }
} // end class Node< T >
```

has two private instance variables—data (of the generic type T) and Node<T> variable nextNode. Variable nextNode references a Node<T> object, an object of the same class being declared here—hence the term “self-referential class.” Field nextNode is a link—it “links” an object of type Node<T> to another object of the same type. Type Node<T> also has five methods: a constructor that receives a value to initialize data, a setData method to set the value of data, a getData method to return the value of data, a setNext method to set the value of nextNode and a getNext method to return a reference to the next node.

Programs can link self-referential objects together to form such useful data structures as lists, queues, stacks and trees. Figure 22.1 illustrates two self-referential objects linked together to form a list. A backslash—representing a null reference—is placed in the link member of the second self-referential object to indicate that the link does not refer to another object. The backslash is illustrative; it does not correspond to the backslash character in Java. We use the null reference to indicate the end of a data structure.

![](img/009e962758dcc71dbc43a493362e6dc0_943_0.png)

Fig. 22.1 | Self-referential-class objects linked together.

## 22.3 Dynamic Memory Allocation

Creating and maintaining dynamic data structures requires dynamic memory allocation—allowing a program to obtain more memory space at execution time to hold new nodes and to release space no longer needed. Remember that Java programs do not explicitly release dynamically allocated memory. Rather, Java performs automatic garbage collection of objects that are no longer referenced in a program.

The limit for dynamic memory allocation can be as large as the amount of available physical memory in the computer or the amount of available disk space in a virtual-memory system. Often the limits are much smaller, because the computer’s available memory must be shared among many applications.

The declaration and class-instance-creation expression

```
// 10 is nodeToAdd's data
Node< Integer > nodeToAdd = new Node< Integer >( 10 );
```

allocates a Node<Integer> object and returns a reference to it, which is assigned to nodeToAdd. If insufficient memory is available, the expression throws an OutOfMemoryError. The sections that follow discuss lists, stacks, queues and trees—all of which use dynamic memory allocation and self-referential classes to create dynamic data structures.
