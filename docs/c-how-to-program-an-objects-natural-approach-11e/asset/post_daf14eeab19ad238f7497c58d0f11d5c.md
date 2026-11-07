
Polymorphic processing. Create a vector of Account pointers to SavingsAccount and CheckingAccount objects. For each Account in the vector, allow the user to specify an amount of money to withdraw and an amount of money to deposit. After processing an Account, print the updated account balance obtained by invoking the base-class member function `getBalance`.

**10.15**  **(Payroll-System Modification)** Modify the payroll system of Section 10.9 to include an additional Employee subclass named HourlyWorker, representing an employee whose pay is based on an hourly wage and the number of hours worked. Hourly workers receive overtime pay (1.5 times the hourly wage) for all hours over 40 hours worked.

Class HourlyWorker should contain private data members `m_wage` (to store the employee’s wage per hour) and `m_hours` (to store the hours worked). Provide a concrete implementation of member function earnings that calculates the employee’s earnings by multiplying the hours worked by the wage per hour. If the number of hours worked is over 40, pay the HourlyWorker for the overtime hours. Add a pointer to an HourlyWorker object into the vector of Employee pointers in `main` and test that the new object works correctly as main polymorphically displays each Employee’s string representation and earnings.

### Programming to an Interface Exercises

**10.16**  **(Programming to an Interface Modification)** Modify the payroll system of Section 10.11 to include the additional CompensationModel subclass Hourly, which determines an employee’s pay based on an hourly wage and the number of hours worked, with 1.5 times the hourly wage for all hours over 40 hours worked. Create an Employee object that gets paid $20 per hour and worked 45 hours. Add the new Employee object to the payroll system’s vector of Employees in `main` to test that your new subclass of CompensationModel works correctly.

**10.17**  **(Project: Refactoring a Class Hierarchy to Use Interface Inheritance and Dependency Injection)** Refactor the Account inheritance hierarchy of Exercises 10.12 and 10.14 to use the interface inheritance and dependency injection techniques from Section 10.11. For this exercise, class Account should be a final class with two data members:

- a `cpp_dec_float_50` (from Boost Multiprecision) for the balance and
- a pointer to an object that implements the AccountModel interface.

The AccountModel interface should have derived classes Savings and Checking to implement the deposit and withdrawal specifics for savings and checking accounts, respectively. Test your refactored code with one Account that uses the Savings model and one that uses the Checking model.

*This page intentionally left blank*

## Operator Overloading, Copy/Move Semantics and Smart Pointers

![](img/7b5e2088e71c7f78681d4ddbcf104c06_645_0.png)

### Objectives

In this chapter, you’ll:

- Use built-in string class overloaded operators.
- Use operator overloading to help you craft valuable classes.
- Understand when to implement the special member functions for custom types.
- Understand when objects should be moved vs. copied.
- Use rvalue references and move semantics to eliminate unnecessary copying when objects go out of scope, improving performance.
- Manage dynamic memory automatically with smart pointers.
- Craft a MyArray class that defines the five special member functions to support copy and move semantics, and overloads many unary and binary operators.
- Use C++20’s three-way comparison operator (<=>).
- Convert objects to other types.
- Use explicit to prevent constructors and conversion operators from being used for implicit conversions.
- Experience a “light-bulb moment” when you’ll truly appreciate the elegance and beauty of the class concept.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_645_1.png)

| Section | Topic | Section | Topic |
|---|---|---|---|
| **11.1** | Introduction | **11.6.6** | Copy Constructor and Copy Assignment Operator |
| **11.2** | Using the Overloaded Operators of Standard Library Class `string` | **11.6.7** | Move Constructor and Move Assignment Operator |
| **11.3** | Operator Overloading Fundamentals | **11.6.8** | Destructor and size functions |
| 11.3.1 | Operator Overloading Is Not Automatic | **11.6.9** | Overloading the Equality (`==`) and Inequality (`!=`) Operators |
| 11.3.2 | Operators That Cannot Be Overloaded | **11.6.10** | Overloading the Subscript (`[]`) Operator |
| 11.3.3 | Operators That You Do Not Have to Overload | **11.6.11** | Overloading the Unary `bool` Conversion Operator |
| 11.3.4 | Rules and Restrictions on Operator Overloading | **11.6.12** | Overloading the Preincrement Operator |
| **11.4** | (Downplaying) Dynamic Memory Management with `new` and `delete` | **11.6.13** | Overloading the Postincrement Operator |
| **11.5** | Modern C++ Dynamic Memory Management: RAII and Smart Pointers | **11.6.14** | Overloading the Addition Assignment Operator (`+=`) |
| 11.5.1 | Smart Pointers | **11.6.15** | Overloading the Binary Stream Extraction (`>>`) and Stream Insertion (`<<`) Operators |
| 11.5.2 | Demonstrating `unique_ptr` | **11.6.16** | friend Function `swap` |
| 11.5.3 | `unique_ptr` Ownership | **11.6.17** | C++20 Three-Way Comparison Operator (`<=>`) |
| 11.5.4 | `unique_ptr` to a Built-in Array | **11.7** | Converting Between Types |
| **11.6** | MyArray Case Study: Crafting a Valuable Class with Operator Overloading | **11.8** | `explicit` Constructors and Conversion Operators |
| 11.6.1 | Special Member Functions | **11.9** | Overloading the Function Call Operator `()` |
| 11.6.2 | Using Class MyArray | **11.10** | Wrap-Up |
| 11.6.3 | MyArray Class Definition |  | Exercises |
| 11.6.4 | Constructor That Specifies a MyArray’s Size |  |  |
| 11.6.5 | Passing a Braced Initializer to a Constructor |  |  |

### 11.1 Introduction

This chapter presents **operator overloading**, which enables C++’s existing operators to work with custom class objects. One example of an overloaded operator in standard C++ is `<<`, which we use as

- the stream insertion operator and
- the bitwise left-shift operator (see the Bit Manipulation appendix at https://deitel.com/cpphtp11).

Similarly, we use `>>` as

- the stream extraction operator and
- the bitwise right-shift operator (see the Bit Manipulation appendix at https://deitel.com/cpphtp11).

You’ve already used many overloaded operators. Some are built into the core C++ language itself. For example, the `+` operator performs differently, based on its context in integer, floating-point and pointer arithmetic with data of fundamental types. Class `string` also overloads `+` to concatenate strings. You can overload most operators for use with custom class objects. The compiler generates the appropriate code based on the operand types. The jobs performed by overloaded operators also can be performed by explicit function calls, but operator notation is often more natural and more convenient.

### String Class Overloaded Operators Demonstration

In Section 2.8, Objects-Natural case study, we introduced the standard library’s `string` class and demonstrated a few of its features, such as string concatenation with the `+` operator. Here, we demonstrate many other string-class overloaded operators, so you can appreciate how valuable operator overloading is in a key standard library class before implementing it in your own custom classes. Next, we’ll present operator-overloading fundamentals.

### Dynamic Memory Management and Smart Pointers

We introduce dynamic memory management, which enables a program to acquire the additional memory it needs for objects at runtime rather than at compile-time and release that memory when it’s no longer needed so it can be used for other purposes. We discuss the potential problems with dynamically allocated memory, such as forgetting to release memory that’s no longer needed—known as a memory leak. Then, we introduce smart pointers, which can automatically release dynamically allocated memory for you. As you’ll see, when coupled with the RAII (Resource Acquisition Is Initialization) strategy, smart pointers enable you to eliminate subtle memory leak issues.

### MyArray Case Study

Next, we present one of the book’s capstone case studies. We build a custom MyArray class that uses overloaded operators and other capabilities to solve various problems with C++’s native pointer-based arrays. We introduce and implement the five special member functions you can define in each class—the copy constructor, copy assignment operator, move constructor, move assignment operator and destructor. Sometimes the default constructor also is considered a special member function. We introduce copy semantics and move semantics, which help tell a compiler when it can move resources from one object to another to avoid costly, unnecessary copies.

MyArray uses smart pointers and RAII, and overloads many unary and binary operators, including

- `=` (assignment)
- `==` (equality)
- `!=` (inequality)
- `[]` (subscript)
- `++` (increment)
- `+=` (addition assignment)
- `>>` (stream extraction) and
- `<<` (stream insertion).

We also show how to define a conversion operator that converts a MyArray to a true or false bool value, indicating whether a MyArray has elements.
