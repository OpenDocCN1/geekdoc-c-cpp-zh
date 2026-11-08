
**Q4.** Evaluate the expression: `!(1 && !(!0 || 1))`.

- i. True
- ii. False
- iii. Results in syntax error

**Q5.** The file `iostream` includes

- i. The declarations of the basic standard input-output library
- ii. The streams of input and output of the program effect
- iii. Both of these
- iv. None of these

**Q6.** Which of the following is not a valid loop structure in C++?

- i. `for`
- ii. `while`
- iii. `do-while`
- iv. `repeat-until`

**Q7.** How many times is a `do-while` loop guaranteed to loop?

- i. 0
- ii. Infinitely
- iii. 1
- iv. Variable – cannot be determined before the loop

**Q8.** Which of the following is known as insertion operator?

- i. `^`
- ii. `||`
- iii. `<<`
- iv. `>>`

**Q9.** Which of the following is an output statement in C++?

- i. `print`
- ii. `write`
- iii. `cin`
- iv. `cout`

**Q10.** The `continue` statement

- i. Resumes the program if it gets hanged
- ii. Resumes the program, if `break` was applied to it
- iii. Skips the rest of the loop in current iteration and goes to the beginning of the block
- iv. All of the above

**Q11.** Which return type should be used before a function name if it does not have a return type?

- i. `int` and return 0 at the end of the function
- ii. No return type
- iii. `void`
- iv. None of these

**Q12.** Functions can be declared with default values in parameters. We use `default` keyword to specify the value of such parameters.

- i. True
- ii. False

## Subjective Questions

- **Q1.** Write a macro definition that obtains the largest of three numbers.
- **Q2.** What is a reference variable? What are its advantages and disadvantages?
- **Q3.** What is the application of scope resolution operator in C++?
- **Q4.** What are the advantages of the `new` operator in comparison to the `malloc` operator?
- **Q5.** Describe the uses of enumeration data type with example.
- **Q6.** What is the application of `void` data type in C++? Illustrate the same with the help of an example.
- **Q7.** Explain how `unsigned int` can be twice as large as `signed int`.
- **Q8.** With the help of an example, illustrate how `setw` manipulator works.
- **Q9.** Write a program in C++ that prevents from buffer overflow while entering a string in a character string buffer using the `setw` manipulator.
- **Q10.** Write a C++ program using predefined preprocessor macros.
- **Q12.** Write a program in C++ to calculate the greatest common divisor of two numbers by using recursive functions.
- **Q13.** Explain the benefits of inline function in C++. Demonstrate how it works using a code flow. List under what conditions the `inline` keyword does not work.
- **Q14.** Write a program in C++ using a string class object. The program should use the string class member functions `rfind()` and `substr()`.
- **Q15.** Demonstrate the usage of reference variables in pass by reference. The example should be different from swapping of variables as shown in this chapter.
- **Q16.** An electricity board charges the following rates to domestic users:

  | Units | Rate |
  |---|---|
  | First 100 units | 60P per unit |
  | Next 200 units | 80P per unit |
  | Beyond 300 units | 90P per unit |

  All users are charged a minimum of Rs. 50.00. If the total amount is more than Rs. 300.00, then an additional surcharge of 15% is added.

  Write a program to read the names of users and number of units consumed and then display the charges with names.

![](img/43c5f409f9b17790a628c4b4df854b61_368_0.png)

## Chapter 13: OOP Principles, Classes and Data Abstraction

| If you need information on: | See page: |
|---|---|
| OOP Principles, Classes and Data Abstraction | 327 |
| Different Paradigms for Problem Solving | 328 |
| Differences between OOP and Procedural Programming | 332 |
| The Concept of Abstraction | 333 |
| Overview of OOP Principles | 335 |
| Encapsulation | 335 |
| Inheritance | 336 |
| Polymorphism | 337 |
| OOP, Objects, and Classes | 340 |
| Constructors | 345 |
| Copy Constructors | 345 |
| Destructors | 348 |
| Class Members | 348 |
| Messages to Objects | 349 |
| Objects | 349 |
| Encapsulation – Access Control to the Members and External Users | 350 |
| Relationships between Classes | 351 |
| Data Abstraction and Information Hiding | 366 |

Object-Oriented Programming (OOP) defines the concepts of classes and objects. A class is a data structure, which closely resembles a real-world entity. It contains data types and methods, which represent the attributes as well as behavior of real-world entities. An object is an instance of the class. The important OOP concepts are data abstraction, encapsulation, and polymorphism. Data abstraction refers to the use of data without knowing how the data is stored or implemented. Encapsulation is the process of hiding those details of an object that do not contribute to the significant characteristics of that object. Polymorphism implies a language’s capability to handle an object differently depending on its runtime. Some examples of OOP languages are C++, Java, and C#.

In this chapter, we first learn about the different paradigms for problem solving. Next, we learn about abstraction as well as the differences between OOP and procedural programming. Then, we get an overview of the OOP principles namely encapsulation, inheritance, and polymorphism. The chapter also discusses OOP, objects, and classes. Further, we learn about constructors, destructors, class members, data abstraction, and information hiding. The chapter also provides the relationships between classes and their components using the diagrammatic representations.

### Different Paradigms for Problem Solving

A programming paradigm is usually a basic style of computer programming. Paradigms for problem solving vary in the concepts and abstractions that are helpful in representing the elements of a program, such as materials, functions, variables, constraints, and the steps that comprise evaluation, continuations, and data streams. Three types of paradigms involved in problem solving are imperative, logical, and functional.

Let’s discuss these three types starting from the imperative programming paradigm.

#### Imperative Programming Paradigm

The imperative programming paradigm signifies how a computer can preserve itself in case any environment variable changes. In other words, if the environment variables change, then a computer can preserve itself so that it does not undergo any functional changes.

In imperative programming, computations are performed by a predefined sequence associated with the steps where environment variables are known or altered. Therefore, the order of the steps is essential because a step may have different consequences with respect to the current values of variables once it is performed. The advantages of the imperative programming paradigm are listed in Figure 13.1:

![](img/43c5f409f9b17790a628c4b4df854b61_369_0.png)

**Figure 13.1: Listing the Advantages of Imperative Programming Paradigm**

![](img/43c5f409f9b17790a628c4b4df854b61_371_0.png)

- The high degree of abstraction.
- The independence of task operations, allowing programs to become evaluated in a variety of orders.
- Popularity.
- The absence of assignment operations can make the function-oriented programs a lot more amenable to numerical proof and evaluation than are imperative programs.

**Figure 13.5: Listing the Advantages of Functional Programming Paradigm**

Disadvantages of the functional programming paradigm are listed in Figure 13.6:

![](img/43c5f409f9b17790a628c4b4df854b61_371_1.png)

- Perhaps less efficiency.
- Problems involving many variables or a lot of sequential activity are sometimes easier to handle imperatively or with object-oriented programming.

**Figure 13.6: Listing the Disadvantages of Functional Programming Paradigm**

Next, let’s discuss the differences between OOP and procedural programming.

### Differences between OOP and Procedural Programming

Procedural programming is a way of coding by identifying a group of steps to solve a particular problem and executing this group of steps in a precise order to reach the required outcome or condition. Suppose we wish to calculate the month-end closing balance for a bank account. The very first step in calculating the balance is to acquire the starting balance from the account and then reducing all the debit amounts occurred throughout the month. After that, we need to add all the credit amounts occurred during the month. At the end of this procedure, we get the month-end closing balance from the account.

One of the main concepts associated with procedural programming is procedure call. A procedure, also called a subroutine, method, or perhaps a function, contains an ordered listing of instructions to be completed. A procedure could be called anytime during the execution of any other procedure or alone. Examples of procedural languages are C and Pascal.

Within OOP, the focus is on taking into consideration the problem to be solved when it comes to real-world elements as well as representing the problem when it comes to objects and their own behavior.

The key distinction between OOP and procedural programming is that the focus of procedural programming would be to break down the actual programming task into an accumulation of variables and subroutines; whereas, the focus of OOP would be to break down the actual programming task into objects, which encapsulate information and methods. Another difference is that procedural programming uses procedures to directly work on data structures; whereas, OOP bundles the information and methods together to ensure that an object will operate on data.

In the next section, let’s discuss abstraction, in detail.
