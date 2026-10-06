
## TWO TRUTHS & A LIE

## Programming

Two of the following statements are true, and one is false. Identify the false statement, and explain why it is false.

- 1. A high-level programming language allows you to use a vocabulary of reasonable terms such as read, write, or add instead of the sequence of on/off switches that perform these tasks.
- 2. Each high-level programming language has its own syntax.
- 3. Programmers use a computer program called a compiler to translate machine code into a high-level language they can understand.

The false statement is #3 Programmers use a compiler to translate their language into machine code.

## Procedural and Object-Oriented Programming

Two popular approaches to writing computer programs are procedural programming and object-oriented programming.

When you write a procedural program, you use your knowledge about programming to create and name memory locations that can hold values, and you write a series of steps or operations to manipulate those values. For example, a simple payroll program might contain instructions similar to the following:

```
get hoursWorked
pay = hoursWorked * 10.00
output pay
```

Named computer memory locations that hold data, such as hoursWorked and pay, are called variables because they hold values that may vary. In programming languages, a variable is referenced by using a one-word name (identifier) with no embedded spaces. For example, the memory location referenced by the name hoursWorked might contain different values at different times for different employees. During the execution of the payroll program, each value stored under the name hoursWorked might have many operations performed on it—for reading from an input device, multiplying it by a rate, and printing it on paper.

Examples of procedural programming languages include C and Logo.

## Procedural and Object-Oriented Programming

For convenience, the individual operations used in a procedural program often are grouped into logical units **methods**. For example, a series of four or five comparisons and calculations that determine an employee's withholding tax value might be grouped as a method named CalculateWithholdingTax().

Capitalizing the first letter of all new words in an identifier, even the first one, as in CalculateWithholdingTax(), is a style called **Pascal casing or upper camel casing**. Although it is legal to start a method name with a lowercase letter, the convention used in C# is for methods to be named using Pascal casing. This distinguishes them from variables, which conventionally use lower casing. Additionally, in C# all method names are followed by a set of parentheses. When this refers to a method, the name will be followed with parentheses.

A procedural program divides a problem into multiple methods, with a unique name. The program then **calls** or **invokes** the methods to input, manipulate, and output the values stored in those locations. A single procedural program often contains hundreds of variables and thousands of method calls.

Depending on the programming language, methods are sometimes called *procedures*, *subroutines*, or *functions*. In C#, the preferred term is *methods*.

| Paycheck |
| :--- |
| payee hoursWorked grossPay |
| calculateAmount() writeCheck() cashCheck() |

**Object-oriented programming (OOP)** is an extension of procedural programming. OOP uses variables and methods like procedural programs, but it focuses on objects that contain variables and methods. An **object** is a concrete entity that has attributes and behaviors. The **attributes of an object** are the values of its attributes which constitute the **state of the object**. For example, attributes of a paycheck include its payee and monetary value, and the state of those attributes are Alice Nelson and $400. The **behaviors of an object** are what it *does*; for example, a paycheck object can be written and cached, and contains a method to calculate the check. Figure-1 shows how a programmer might start to visualize a paycheck—thinking about its name, attributes, and behaviors.

**Figure 1-1** A diagram for a Paycheck

Beyond a paycheck, object-oriented programs might design a payroll system by thinking about all the objects needed to produce a paycheck, such as employees, time cards, and bank accounts.

Programmers use the term OO, pronounced "oh oh," as an abbreviation for object-oriented programming; they use OO, which rhymes with soup. Examples of OO languages include C#, Java, and C++. You can write procedural programs in OO languages, but not OO programs in procedural languages.

## CHAPTER 1 A First Program Using C#

With each approach, procedural or object-oriented, you can produce a correct paycheck, and both techniques employ reusable program modules. The major difference lies in the focus the programmer takes during the earliest stages of a project. Taking an object-oriented approach to a problem means defining the objects needed to accomplish a task and developing classes that describe the objects so that each object maintains its own data and carries out tasks when another object requests them. The object-oriented approach is said to be “natural”—it is more common to think of a world of objects and the ways they interact than to consider a system of functions, data items, and the logic required to manipulate them.

Object-oriented programming employs a large vocabulary; you can learn much of this terminology in the chapter called “Using Classes and Objects."

Originally, object-oriented programming was used most frequently for two major types of applications:

- Computer simulations are programs that attempt to mimic real-world activities so that their processes are improved or so that users can understand how the real-world processes operate.
- Graphical user interfaces, or GUIs (pronounced goys) are programs that allow users to interact with a program in a graphical environment, such as clicking with a mouse or using a touch screen.

Thinking about objects in these two types of applications makes sense. For example, a city might want to develop a program that simulates traffic patterns to prevent congestion. By creating a model with objects, the simulation can be more accurate. For example, a city might want to develop a program that simulates traffic patterns to prevent congestion. By creating a model with objects, the simulation can be more accurate. For example, a city might want to develop a program that simulates traffic patterns to prevent congestion. By creating a model with objects, the simulation can be more accurate. For example, a city might want to develop a program that simulates traffic patterns to prevent congestion. By creating a model with objects, the simulation can be more accurate. For example, a city might want to develop a program that simulates traffic patterns to prevent congestion. By creating a model with objects, the simulation can be more accurate. For example, a city might want to develop a program that simulates traffic patterns to prevent congestion. By creating a model with objects, the simulation can be more accurate. For example, a city might want to develop a program that simulates traffic patterns to prevent congestion. By creating a model with objects, the simulation can be more accurate.
