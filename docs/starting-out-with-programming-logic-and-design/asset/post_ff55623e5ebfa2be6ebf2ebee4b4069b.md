
doubleNumber module, which causes the number variable’s contents to be copied into the value parameter variable. This is shown in Figure 3-13.

## Program 3-6

```
Module main()
  Declare Integer number
  Display "Enter a number and I will display"
  Display "that number doubled."
  Input number
  Call doubleNumber(number)
  End Module

Module doubleNumber(Integer value)
  Declare Integer result
  Set result = value * 2
  Display result
  End Module
```

## Program Output (with Input Shown in Bold)

Enter a number and I will display
that number doubled.
20 [Enter]

Figure 3-13 The contents of the number variable passed as an argument

![](img/c939132f78787c7f339c6977b3fc8c85_124_0.png)

## Argument and Parameter Compatibility

When you pass an argument to a module, most programming languages require that the argument and the receiving parameter be of the same data type. If you try to pass an argument of one type into a parameter of another, an error usually occurs. For example, Figure 3-14 shows that you cannot pass a real number or a Real variable into an Integer parameter.

## 3.4 Passing Arguments to Modules

### Figure 3-14 Arguments and parameter variables must be of the same type

```
Call doubleNumber(55,9)
Declare Real number = 24.7
Call doubleNumber(number)
Error!
Error!
Module doubleNumber(Integer value)
Declare Integer result
Set result = value * 2
Display result
End Module
Module doubleNumber(Integer value)
Declare Integer result
Set result = value * 2
Display result
End Module
```

![](img/c939132f78787c7f339c6977b3fc8c85_125_0.png)

> NOTE: Some languages allow you to pass an argument into a parameter variable of a different type as long as no data will be lost. For example, some languages allow you to pass integer arguments into real parameters because real variables can hold whole numbers. If you pass a real argument, such as 24.7, into an integer parameter, the fractional part of the number would be lost.

![](img/c939132f78787c7f339c6977b3fc8c85_125_1.png)

## Parameter Variable Scope

Earlier in this chapter, you learned that a variable's scope is the part of the program in which it may be accessed. A variable is visible only to statements inside the variable's scope. A parameter variable's scope is entirely the module in which the parameter is declared. No statement outside the module can access the parameter variable.

## Passing Multiple Arguments

Most languages allow you to write modules that accept multiple arguments. Program 3-7 shows a pseudocode module showSum that accepts two Integer arguments. The module adds the two arguments and displays their sum.

## Program 3-7

```
1 Module main()
2 Display "The sum of 12 and 45 is:"
3 Call showSum(12, 45)
4 End Module
6 Module showSum(Integer num1, Integer num2)
7 Declare Integer result
8 Set result = num1 + num2
9 Display result
10 End Module
```

![](img/c939132f78787c7f339c6977b3fc8c85_125_2.png)

## Program Output

The sum of 12 and 45 is:
57

Notice that two parameter variables, num1 and num2, are declared inside the parentheses in the module header. This is often referred to as a parameter list. Also notice that a comma separates the declarations.

## Chapter 3 Modules

The statement in line 3 calls the showSum module and passes two arguments: 12 and 45. The arguments are passed into the parameter variables in the order that they appear in the module. In other words, the first argument is passed into the first parameter variable, and the second argument is passed into the second parameter variable. So, this statement clauses 12 to be passed into the num1 parameter and 45 to be passed into the num2 parameter, as shown in Figure 3-15.

### Figure 3-15 Two arguments passed into two parameters

```
Module main())
    Display "The sum of 12 and 45 is:"
    Call showSum(12, 45)
End Module

Module showSum(Integer num1, Integer num2)
    Declare Integer result
    Set result = num1 + num2
    Display result
End Module
```

When we want to reverse the order in which the arguments are listed in the module, as shown here:

Call showSum(45, 12)

This would cause 45 to be passed into the num1 parameter and 12 to be passed into the num2 parameter. The following pseudocode code shows one example. This time we are passing as arguments.

```
Declare Integer value1 = 2
Declare Integer value2 = 3
Call showSum(value1, value2)
```

When the showSum method executes as a result of this code, the num1 parameter will contain 2 and the num2 parameter will contain 3.

> In the Spotlight: Passing an Argument to a Module
> Your friend Michael runs a catering company. Some of the ingredients his recipes are measured in cups. When he goes to the grocery store to buy those ingredients, however, are sold only by ounce. He has asked you to write a simple program that converts cups to ounces.
> You design the following algorithm:
> - Display an introductory screen that explains what the program does.
> - Get the number of cups.
> - Convert the number of cups to ounces and display the result.
> This algorithm lists the top level of tasks that the program needs to perform, and becomes the basis of the program’s main module. Figure 3-16 shows the program’s structure in hierarchy chart.

![](img/c939132f78787c7f339c6977b3fc8c85_126_0.png)
![](img/c939132f78787c7f3fc85_127_0.png)

As shown in the hierarchy chart, the main module will call two other modules. Here are summaries of these modules:
- showIntro—This module will display a message on the screen that explains what the program does.
- cupsounces—This module will accept the number of cups as an argument and calculate and display the equivalent number of ounces.

In addition to calling these modules, the main module will ask the user to enter the number of cups. This value will be passed to the cupsounces module. Program 3-8 shows the pseudocode for the program, and Figure 3-17 shows a flowchart.

## Program 3-8

```
1 Module main()
2 // Declare a variable for the
3 // number of cups needed.
4 Declare cupsNeeded
5
6 // Display an message.
7 Call showIntro()
8
9 // Get the number of cups.
10 Display "Enter the number of cups."
11 Input cupsNeeded
12
13 // Convert cups to ounces.
14 Call cupsounces(cupsNeeded)
15 End Module
16
17 // The showIntro module displays an
18 // introductory screen.
19 Module showIntro()
20 Display "This program converts measurements"
21 Display "in cups ounces. For your"
22 Display "reference the formula is:"
23 Display "1 cup = 8 ounces."
24 End Module
25
26 // The cupsounces module accepts a number
27 // of cups and displays the equivalent number
28 Module cupsounces(Real cups)
29 // Declare variables.
30 Declare Real ounces
31
32 // Convert cups to ounces.
33 Set ounces = cups * 8
34
35 // Display the result.
36 Display "That converts to "
37 Display "ounces."
38 End Module
```

## Program Output (with Input Shown in Bold)

This program converts measurements
in cups to fluid ounces. For your
reference the formula is:
1 cup = 8 ounces.
Enter the number of cups.
**[Enter]**
That converts to 8 ounces.

3-17 Flowchart for Program 3-8

![](img/c939132f78787c7f339c6977b3fc8c85_128_0.png)

## Passing Arguments by Value and by Reference

Many programming languages provide two different ways to pass arguments: by value and by reference. Before studying these techniques in detail, we should mention that different languages have their own way of doing each. In this book, we will teach you the fundamental concepts behind these techniques, and show you how to model them in pseudocode. When you begin to use these techniques in an actual language, you will need to learn the details of how they are carried out in that language.

## Passing Arguments by Value

All of the examples that we have looked at far pass arguments by value. Arguments and parameter variables are separate items in memory. Passing arguments by value means that only a copy of the value is passed into the parameter variable. If the contents of the variable are changed inside the module, it has no effect on the calling part of the program. For example, look at Program 3-9.

## Program 3-9

```
Module main()
    Declare Integer number = 99

    // Display the value stored in number.
    Display "The number is ", number

    // Call the changeMe module, passing
    the number variable as an argument.
    Call changeMe(number)

    // Display the value of number again.
    Display "The number is ", number
    End Module

Module changeMe(Integer myValue)
    Display "I am changing the value."

    // Set the myValue parameter variable
    // to 0.
    Set myValue = 0

    // Display the value in myValue.
    Display "Now the number is ", myValue
    End Module
```

## Program Output

The number is 99
I am changing the value.
Now the number is 0
The number is 99

The main module declares a local variable named number in line 2, and initializes it to the value 99. As a result, the Display statement in line 5 displays "The number is 99."
The variable's value is then passed as an argument to the changeMe module in
