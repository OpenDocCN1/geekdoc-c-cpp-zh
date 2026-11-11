
## 01 | Structured Programming with C++

**OBJECTIVES**

- 1.1 Introduction to C++
- 1.2 History of C++
- 1.3 C++: Superset of the C Programming Language
- 1.4 Exploring the Basic Components of C++

C++ is a popular Object-Oriented Programming (OOP) language that has evolved from the C language. Earlier, the C language was used to create computer programs. However, there were several problems with programming in C. One of the problems was that various functions in a C program were linked with each other and if an error occurred in any one of them, it became difficult for a programmer to locate the function and rectify the error. Another problem with the C language was that the code written in one program could not be used for another program. In addition, there were also security-related concerns in the C language. As the data was globally shared, it could easily be accessed by any function in a program and any modification in that data affected the functioning of the entire program. C++, which is an object-oriented language, emerged as a solution for these problems.

This chapter introduces the features of OOP in C++ and also discusses the C++ language, its history, features and advantages. In this chapter, you also learn about C++ as the superset of the C programming language and explore the basic components of the C++ language.

### 1.1 | Introduction to C++

C++ implements the concept of objects in the programming world. An object in the real world can be any entity that has its own attributes. For example, a pen is a real-world entity, which has attributes, such as shape, color, and durability. There are various types of pens, such as Reynolds and Rotomac; however, not all of these pens are the same. These pens have their own attributes. Now, if we want to relate these pens to the programming world, they would be known as the objects of the pen class. An object can inherit some of the class attributes, though it also has its own attributes. For example, every pen should have a color and a shape; therefore, color and shape become the attributes of the pen class. Now, the color and shape of a pen may vary from pen to pen; therefore, color and shape become the attributes of the type of pen that is the object of the pen class. Inheriting the attributes of a class allows code reusability, which means that there is no need to rewrite code, which is already available to implement the functionality of the inherited class. This feature of C++ makes it easy to manage large programs. Moreover, in OOP the different objects of a class are independent of each other, which implies that the changes in one object do not affect the functionality of other objects.

Now that you have a basic idea of the C++ language, let's discuss the history of this language.

### 1.2 History of C++

Bjarne Stroustrup at AT&T Bell Laboratories developed an enhancement of C named *C with Classes* in 1979. Later, in 1983, it was renamed to C++ and is used internally at AT&T. C++ is derived from the C language. The concepts of OOP were implemented in the C language, and then C developed into an OOP language called C++. In fact, C++ is also known as a superset of the C language, because C++ includes all the functionalities of the C language. Bjarne Stroustrup called it C with Classes, which was later changed to C++. The ++ sign of C++ denotes the increment operator of the C language and is appended in C to emerge a new name, C++, as C++ is derived from the C language.

C++ was developed to create easily manageable and reusable programs. The C language was popular before the development of C++ and was considered a very good programming language at that time. However, managing long programs in the C language was a problem since all the functions in a C program are interrelated and the changes made in one function affect the performance of other functions. In such a scenario, it was not easy for a programmer to find out the function in which a problem had occurred. This was why a need for a new programming language was felt, a programming language in which the fragments of the program code worked independently so that a program could be managed easily.

After understanding the history and emergence of C++, let's analyze the C language as a procedure-oriented language and C++ as an object-oriented language, under the following subheadings:

- C: Procedure-Oriented Programming
- C++: Object-Oriented Programming

#### C: Procedure-Oriented Programming

The C language was the most popular programming language of the 1970s and it brought about a revolution in the programming world. The programming languages before C used code and mnemonics, but with the evolution of C, programming is done with the help of a few statements, such as `printf`, `scanf`. Writing a program by using these statements is much easier than writing a program using codes and mnemonics. This was the reason for the popularity of C.

C is a procedure-oriented programming language in which a program is divided into various parts called procedures and functions. This simply means that instead of creating a large program, various small procedures that perform specific tasks, such as adding numbers and calculating interest, can be created separately by programmers. The following are the characteristics of procedure-oriented languages:

- Emphasis on the algorithm to perform a task
- Division of programs into small procedures to perform various tasks
- Sharing of global data among procedures
- Passing of parameters between various procedures to allow the procedures to communicate with each other
- Support for user-defined data types

In a C program, several procedures and functions share global data, although they can also have local data. Sharing global data by various procedures and functions increases the complexity of a program. Global data can easily be changed by any function in the program, which may affect the functionality of the other functions sharing the same data. Therefore, sharing of global data is the main drawback of the C language. A programmer can overcome the problems that occur due to global data sharing by remembering what data is used by which function. However, this is a very tedious task. As a result, to permanently overcome this problem, the concept of OOP was brought into the programming world.

Now, let's discuss the features and advantages of OOP.

#### C++: Object-Oriented Programming

OOP is used to create more reliable and reusable programs. It binds the data and code together and treats them as a single entity. OOP also helps a programmer create a modular program, which consists of reusable code that can easily be used in creating other programs. The functionality of reusing the code helps in creating software applications quickly and with less cost. In OOP, we follow the bottom-up approach, that is, a large program is created by combining various small functioning units.

Now, let's discuss the features and advantages of OOP in the following sections.

##### Features of OOP

The following are some of the important features of OOP:

- **Encapsulation**: Allows binding of class members (variables and methods) together and protects them from being accessed by the other classes. In C++, encapsulation is implemented by using a construct called `class`. An instance of a class is known as `object`, which is used to invoke various functions in a program.
- **Data Abstraction**: Allows hiding of data not required by a user to perform some specific functioning. In C++, a class is used to implement data abstraction, which is one of the most powerful features of OOP.

```c
printf ("Hello from C.");
return 0;
}
```

The same program can be written in C++, as shown in Listing 2 (you can find the Welcome.cpp file on the CD in the code/chapter1 folder):

**▶ Listing 2: Displaying a C++ Program**

```cpp
#include <iostream.h>

// display a welcoming message.
int main() {
    cout << "Hello from C++." << endl;
    return 0;
}
```

Let's compare both the C and C++ programs defined in the two preceding listings to understand how C++ is a superset of C.

In both Listing 1 and Listing 2, the #include preprocessor directive is used in the very first line. The #include preprocessor directive is used to insert the specified header files so that the C/C++ compiler knows the methods and objects included in the program.

Moreover, you must have noticed in Listing 1 and Listing 2 that the main() function is written, which is the entry point of a C/C++ program. The main() function is followed by a pair of curly braces { }, which includes all the code related to a C/C++ program.

In a C program, we use the printf() function to display the output, while the cout object is used in C++. You can also use the printf function in C++ to display the output, but the cout object is much more flexible than the printf function.

> *Refer to the Writing a C++ Program section to know more about the cout object*

Let's now move ahead to get some in-depth knowledge about C++. In the following sections, you learn about some of the commonly used terms in C++ and also about library functions and linkers. In addition, you learn to create and execute a simple program in C++. These topics are all taken up under the following broad level heads:

- Explaining commonly-used terms in C++
- Exploring the C++ library functions and linkers
- Compiling and running C++ programs

#### Commonly Used Terms in C++

There are many terms in every programming language but a few of them are most commonly used. C++ also has some commonly used terms. The following is a brief description of such terms:
