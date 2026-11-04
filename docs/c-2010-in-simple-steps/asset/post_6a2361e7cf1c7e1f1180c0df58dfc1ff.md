
## Summary

In this chapter, you have learned about:

- Relationship between C# and .NET Framework 4.0
- New features introduced in C# 2010, such as dynamic types, named and optional arguments, enhanced COM interoperability, covariance and contravariance, new command-line compiler options, and implicit line continuations
- Different types of keywords in C# 2010 such as reserved keywords and contextual keywords
- Different data types in C# 2010, such as value types, reference types, and pointer types
- Variables and constants and how these can be declared and used in an application
- Operators and the way these are used in an application
- The conversion of one data type to another by using type conversion, casting techniques, and boxing and unboxing
- Enumerations and how to create them
- Arrays and their different types, such as single-dimensional, multidimensional, and jagged arrays

## Chapter 3

### Working with Control Structures and Exception Handling

In this Chapter:

- Working with Statements
- Working with Selection Statements
- Exploring Loops or Iteration Statements
- Exploring Jump Statements
- Working with Exception
- Commenting a C# Program

The flow of a program written in any programming language implies the way in which the program executes. Normally, a program written in C# executes in a sequential manner. In case you want to change the flow of execution of the program, you need to use the control flow statements, such as if else and switch statements. The control flow statements change the flow of execution of a program according to your requirements. For instance, you can use the control flow statements to execute only specific blocks of code on the fulfillment of specific conditions. You can also use the control flow statements to transfer the program control from one block of code to another.

Sometimes a situation may occur when your program is logically correct and compiles successfully, but it fails to display the required output and terminates abruptly. Such kind of situations may arise due to an exception in your program. An abnormal condition that often occurs while a program is being executed and disrupts the normal flow of application is known as an exception.

In this chapter, you learn how to work with the different statements used in C#, such as selection statements, iteration statements, and jump statements. You also learn about exceptions and how to handle them. In the end, you learn about comments, their types, and how to add comments to a C# program.

Let's start by learning how to work with different statements in C#.

### Working with Statements

In C#, statements serve as building blocks for any program. You can perform varied functions with the help of statements, such as declaring a local variable (a variable which is defined inside a method and has no presence outside the method), calling a method, and creating an object. In C#, some of the most commonly used statements are as follows:

- **Simple statement:** Consists of a single line of code. It is terminated by a semicolon. The following code snippet shows an example of a simple statement:

  ```csharp
  int var1 = 5;
  ```

- **Compound statement:** Consists of more than one statement enclosed in braces. A compound statement is sometimes also called a block statement and usually appears as the body of another statement, such as the if statement.
- **Empty statement:** Specifies that no operations are required to be performed but a statement is required. You can specify an empty statement by a single semicolon. For example, the following code snippet shows the use of the empty statement:

  ```csharp
  void login() {
      if (x > 3) goto exit;
      // ...
      exit: ;
  }
  ```

- **Expression statement:** Evaluates an expression and stores the resulting value in a variable. An expression statement is shown in the following code snippet:

  ```csharp
  float volume = length * breadth * height; // assigns the volume of a cuboid to the float variable volume
  ```

- **Selection statement:** Enables you to control the flow of program execution depending on one or more conditions or criteria. The if...else and switch statements are the examples of selection statements used in C#.
- **Iteration statement:** Allows you to repeatedly perform a specified task(s) until certain condition is reached. The examples of iteration statements are **for**, **while**, **do...while**, and **foreach** loops.
- **Jump statement:** Transfers the program control to a different section of code. The **break**, **continue**, **goto**, **default**, and **return** statements are examples of the jump statements.

**Note**

You learn about the selection statements, iteration statements, and jump statements in detail later in this chapter.

Let's now learn about the selection statements.

### Working with Selection Statements

In C#, the statements that cause the flow of a program to change based on a certain condition are known as selection statements. The program control checks a condition before executing the code inside the selection statement. The selection statement causes the program control to adopt a specific flow of execution based on whether or not a certain condition is true. C# supports the following two types of selection statements:

- **if statement:** Allows you to test whether or not a certain condition is true. If the condition is true, the program control is transferred to the block of code that is inside the **if** statement; otherwise, the program control is transferred to another block of code.
- **switch statement:** Allows you to compare an expression with different values.

Now, let's discuss each of these selection statements in detail.

### The if Statement

One of the most important and commonly used selection statement in C# is the **if** statement. The **if** statement evaluates a specified condition or a set of conditions to true or false. If the condition is true, the program control enters the **if** block and executes all the statements and instructions inside the **if** block. The syntax of the **if** statement is as follows:

```csharp
if (condition) { // condition
    // statement
}
```

In the preceding syntax, if the condition inside the **if** block is evaluated to true, then the program control is transferred to the statements inside the **if** block and executes the statements.

Now, let's create a console application named **If Example** to learn how to use the **if** statement. Perform the following steps to create the **If Example** application:

1. Click Start → All Programs → Microsoft Visual Studio 2010 → Microsoft Visual Studio 2010 to open the Visual Studio 2010 integrated development environment (IDE).
2. Select File → New → Project from the menu bar.

   The New Project dialog box appears.
3. Select Visual C# from the Installed Templates pane and then select the Console Application option from the middle pane of the New Project dialog box.
4. Enter If Example in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box. In this case, we have selected the location, D:\C#2010 Applications.
5. Click the OK button. The If Example application is created, as shown in Fig.C#-3.1:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_85_0.png)

**Fig.C#-3.1**

As you can see in Fig.C#-3.1, whenever you create a console application in Visual Studio 2010, the Visual Studio IDE automatically generates some files for your application. The first is the Properties file, which contains the configuration, security, and deployment options that you can apply to your entire console application. For example, you can set the properties for your entire application in the Properties file to indicate whether a file should be compiled or embedded into the build output as a resource. The second file is the References file that identifies a binary file, which is required to run the application. In other words, it contains the references of all the assemblies that are required by your application. The third file is the Program.cs file, which is the source code file where you actually write the code for an application. The Program.cs file contains the entry point for an application.

6. Add the highlighted code given in Listing 3.1 in the Program.cs file of the If Example application:

   ### Listing 3.1: Using the if Statement

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   namespace IfExample
   {
       class Program
       {
           static void Main(string[] args)
           {
               int num;
               Console.WriteLine("Please enter a number:");
               num = Convert.ToInt32(Console.ReadLine());
               if (num % 2 == 0)
               {
                   Console.WriteLine("The number entered is even");
               }
               Console.ReadLine();
           }
       }
   }
   ```

In Listing 3.1, the Console.ReadLine() method is used to take input from a user, which is stored in the variable, num. The if statement checks the number entered by the user. If the number is divisible by 2, then the statement inside the if block is executed. In case, the user enters a number that is not divisible by two; no output is displayed, because there is no condition set for this.

7. Press the F5 key to run the If Example application. The output appears, as shown in Fig.C#-3.2:
