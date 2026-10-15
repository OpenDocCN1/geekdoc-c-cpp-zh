

1. *用例图*，例如图 2.14 所示，描述系统与其外部实体（参与者）在用例（系统能力，例如“查看账户余额”、“取款”和“存款”）方面的交互。
2. *类图*，你将在第 3.11 节学习，描述系统中使用的类，或“构建块”。需求规格说明书中描述的每个名词或“事物”都是系统中类的候选（例如，“账户”、“键盘”）。类图帮助我们指定系统各部分之间的结构关系。例如，ATM 系统类图将指定 ATM 在物理上由屏幕、键盘、现金 dispenser 和存款槽组成。
3. *状态机图*，你将在第 5.10 节学习，描述对象状态变化的方式。对象的*状态*由对象所有属性在给定时间的值指示。当对象状态发生变化时，该对象在系统中的行为可能不同。例如，在验证用户 PIN 后，ATM 从“用户未认证”状态转换到“用户已认证”状态，此时 ATM 允许用户执行金融交易（例如，查看账户余额、取款、存款）。
4. *活动图*，你也将在第 5.10 节学习，描述对象的*活动*——程序执行期间对象的 workflow（事件序列）。活动图描述对象执行的操作并指定执行这些操作的顺序。例如，活动图显示 ATM 必须先获取用户账户的余额（来自银行的账户信息数据库），屏幕才能向用户显示余额。
5. *通信图*（在 UML 早期版本中称为*协作图*）描述系统中对象之间的交互，重点在于*发生*了哪些交互。你将在第 7.12 节看到，这些图显示执行 ATM 交易时必须交互哪些对象。例如，ATM 必须与银行的账户信息数据库通信以检索账户余额。
6. *序列图*也描述系统中对象之间的交互，但与通信图不同，它们强调交互发生的*时间*。你将在第 7.12 节看到，这些图有助于显示执行金融交易时交互发生的顺序。例如，屏幕在现金 dispenser 前提示用户输入取款金额。

在第 3.11 节，我们通过从需求规格说明书中提取关键名词和名词短语来继续设计我们的 ATM 系统，从而识别出需求规格说明书中的类。利用这些类，我们开发了 ATM 系统结构的第一版类图。

## Web Resources

以下 URL 提供有关使用 UML 进行面向对象设计的信息。
www.objectsbydesign.com/books/booklist.html
列出有关 UML 和面向对象设计的书籍。
www-306.ibm.com/software/rational/offerings/design.html
提供有关 IBM Rational 软件用于设计系统的信息。提供 30 天试用版产品的下载，例如 IBM Rational Application Developer。

- b) Sequence diagrams
- c) Communication diagrams
- d) Activity diagrams

## 2.3 Which of the following choices lists stages of a typical software life cycle in sequential order?

- a) design, analysis, implementation, testing
- b) design, analysis, testing, implementation
- c) analysis, design, testing, implementation
- d) analysis, design, implementation, testing

## Answers to Software Engineering Case Study Self-Review Exercises

2.1 Figure 2.15 shows a use case diagram for a modified version of our ATM system that also allows users to transfer money between accounts.

2.2 b.

2.3 d.

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_89_0.png)

Fig. 2.15 | Use case diagram for a modified version of our ATM system that also allows users to transfer money between accounts.

## 2.8 Wrap-Up

You learned many important basic features of C++ in this chapter, including displaying data on the screen, inputting data from the keyboard and declaring variables of fundamental types. In particular, you learned to use the output stream object cout and the input stream object cin to build simple interactive programs. We explained how variables are stored in and retrieved from memory. You also learned how to use arithmetic operators to perform calculations. We discussed the order in which C++ applies operators (i.e., the rules of operator precedence), as well as the associativity of the operators. You also learned how C++’s if statement allows a program to make decisions. Finally, we introduced the equality and relational operators, which you use to form conditions in if statements.

The non-object-oriented applications presented here introduced you to basic programming concepts. As you’ll see in Chapter 3, C++ applications typically contain just a few lines of code in function main—these statements normally create the objects that perform the work of the application, then the objects “take over from there.” In Chapter 3, you’ll see how to implement your own classes and use objects of those classes in applications.

## 3

Introduction to
Classes and
Objects

## OBJECTIVES

In this chapter you’ll learn:

- What classes, objects, member functions and data members are.
- How to define a class and use it to create an object.
- How to define member functions in a class to implement the class’s behaviors.
- How to declare data members in a class to implement the class’s attributes.
- How to call a member function of an object to make that member function perform its task.
- The differences between data members of a class and local variables of a function.
- How to use a constructor to ensure that an object’s data is initialized when the object is created.
- How to engineer a class to separate its interface from its implementation and encourage reuse.

> Nothing can have value without being an object of utility.
> 
> —Karl Marx
> 
> Your public servants serve you right!
> 
> —Adlai E. Stevenson
> 
> Knowing how to answer one who speaks, To reply to one who sends a message.
> 
> —Amenemope
> 
> You’ll see something new. Two things. And I call them Thing One and Thing Two.
> 
> —Dr. Theodore Seuss Geisel

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_90_0.png)

- 3.1 Introduction
- 3.2 Classes, Objects, Member Functions and Data Members
- 3.3 Overview of the Chapter Examples
- 3.4 Defining a Class with a Member Function
- 3.5 Defining a Member Function with a Parameter
- 3.6 Data Members, set Functions and get Functions
- 3.7 Initializing Objects with Constructors
- 3.8 Placing a Class in a Separate File for Reusability
- 3.9 Separating Interface from Implementation
- 3.10 Validating Data with set Functions
- 3.11 (Optional) Software Engineering Case Study: Identifying the Classes in the ATM Requirements Specification
- 3.12 Wrap-Up

## 3.1 Introduction

In Chapter 2, you created simple programs that displayed messages to the user, obtained information from the user, performed calculations and made decisions. In this chapter, you'll begin writing programs that employ the basic concepts of object-oriented programming that we introduced in Section 1.10. One common feature of every program in Chapter 2 was that all the statements that performed tasks were located in function main. Typically, the programs you develop in this book will consist of function main and one or more classes, each containing data members and member functions. If you become part of a development team in industry, you might work on software systems that contain hundreds, or even thousands, of classes. In this chapter, we develop a simple, well-engineered framework for organizing object-oriented programs in C++.

First, we motivate the notion of classes with a real-world example. Then we present a carefully paced sequence of seven complete working programs to demonstrate creating and using your own classes. These examples begin our integrated case study on developing a grade-book class that instructors can use to maintain student test scores. This case study is enhanced over the next several chapters, culminating with the version presented in Chapter 7, Arrays and Vectors. We also introduce the C++ standard library class string in this chapter.

## 3.2 Classes, Objects, Member Functions and Data Members

Let’s begin with a simple analogy to help you reinforce your understanding from Section 1.10 of classes and their contents. Suppose you want to drive a car and make it go faster by pressing down on its accelerator pedal. What must happen before you can do this? Well, before you can drive a car, someone has to design it and build it. A car typically begins as engineering drawings, similar to the blueprints used to design a house. These drawings include the design for an accelerator pedal that the driver will use to make the car go

