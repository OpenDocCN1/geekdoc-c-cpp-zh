
2. Add the constructor shown in bold in the code that follows to the Complex struct, immediately after the existing constructor and before the ToString method. This new constructor takes a single int parameter, which it uses to initialize the Real property. The Imaginary property is set to 0.

Click here to view code image

```sharp
struct Complex
{
    public Complex(int real)
    {
        this.Real = real;
        this.Imaginary = 0;
    }
}
```

3. Add the following implicit conversion operator shown in bold to the Complex struct:

Click here to view code image

```sharp
struct Complex
{
    public static implicit operator Complex(int from) => new Complex(from);
}
```

This operator converts from an int to a Complex object by returning a new instance of the Complex struct built using the constructor you created in the previous step.

4. Add the following explicit conversion operator shown in bold to the Complex struct:

Click here to view code image

```sharp
struct Complex
{
    ......
```

```sharp
public static explicit operator int(Complex from) =>
from.Real;
  ...
}
```

This operator takes a Complex object and returns the value of the Real property. This conversion discards the imaginary element of the complex number.

+ 5. Display the Program.cs file in the Code and Text Editor window. Then add the following code shown in bold to the end of the doWork method:

Click here to view code image

```sharp
static void doWork() {
  ...
  Console.WriteLine("Current value of temp is {temp}");
  if (temp == 2) {
    Console.WriteLine("Comparison after conversion: temp == 2");
  } else {
    Console.WriteLine("Comparison after conversion: temp != 2");
  }
  temp += 2;
  Console.WriteLine("Value after adding 2: temp = {temp}");
}
```

These statements test the implicit operator that converts an int to a Complex object. The if statement compares a Complex object to an int. The compiler generates code that converts the int into a Complex object first and invokes the == operator of the Complex struct. The statement adds 2 to the temp variable converts the int value 2 into a Complex object and uses the + operator of the Complex struct.

Click here to view code image

```sharp
static void doWork()
{
    int tempInt = temp;
    Console.WriteLine($"Int value after conversion: tempInt == {tempInt}");
}
```

The first statement attempts to assign a Complex object to an int variable.
The second statement displays the result.

+ 7. On the Build menu, select Rebuild Solution.

The solution fails to build, and the compiler reports the following error
in the Error List window:

Click here to view code image

Cannot implicitly convert type 'ComplexNumbers.Complex' to
'int'. An explicit conversion
exists (are you missing a cast?)

The operator that converts from a Complex object to an int is an explicit
conversion operator, so you must specify a cast.

+ 8. Modify the statement that attempts to store a Complex value in an int
variable to use a cast, like this:

int tempInt = (int)temp;

9. On the Debug menu, select Start Without Debugging. Then verify that
the solution builds and the final four messages displayed look like
this:

Click here to view code image

Current value of temp is (2 + 0i)
Comparison after conversion: temp == 2
Value after adding 2: temp = (4 + 0i)
Int value after conversion: tempInt == 4

+ 10. Close the application, and return to Visual Studio 2022.

# Summary

In this chapter, you learned how to overload operators and provide functionality specific to a class or structure. You implemented several common arithmetic operators, and you created operators with which you can compare instances of a class. Finally, you learned how to create implicit and explicit conversion operators.

+ - If you want to continue to the next chapter, keep Visual Studio 2022 running and turn to Chapter 23, “Improving throughput by using tasks.”
- If you want to exit Visual Studio 2022 now, on the File menu, select Exit. If you see a Save dialog, select Yes and save the project.

# Quick reference

| To | Do this |
| --- | --- |
| Implement operator | Write the keywords public and static, followed by the return type, followed by the operator keyword, followed by the operator symbol being declared, followed by the appropriate parameters between parentheses. Implement the logic for the operator in the body of the method. For example: | [Click here to view code image]
```cpp
struct Complex {
    ...
    public static bool operator ==(Complex lhs, Complex rhs)
    {
        ...\ // Implement logic for == operator
        ...
    }
}
``` |
| Define a conversion operator | Write the keywords public and static, followed by the conversion keyword implicit or explicit, followed by the operator keyword, followed by the type the data is being converted to, followed by the type the data is being converted from as a single parameter between parentheses. For example: | Click here to view code image

```sharp
struct Complex
{
    public static implicit operator Complex(int from)
    {
        ... // code to convert from an int
    }
}
``` |

# Building Universal Windows Platform applications with C#

+ - CHAPTER 23 Improving throughput by using tasks
- CHAPTER 24 Improving response time by performing asynchronous operations
- CHAPTER 25 Implementing the user interface for UWP app
- CHAPTER 26 Displaying and searching for data in UWP app
- CHAPTER 27 Accessing a remote database from UWP app

So far, you've gained a thorough grounding in the syntax and semantics of the C# language. It's now time to examine how you can use this knowledge to take advantage of the features Windows provides for building applications. UWP applications can detect and adapt to the hardware on which they execute. You can also build cloud-connected applications; these applications are not tied to a specific computer but follow users when they sign in on another device. In short, Visual Studio 2022 provides the tools for developing highly mobile, highly graphical, highly connected applications that can run anywhere.

Part IV introduces you to the requirements of building UWP applications.
You'll see examples of the asynchronous model of programming developed as part of .NET. You'll also learn how to build a UWP application that connects to the cloud to retrieve and present complex information in a natural and easily navigable style.

# Chapter 23

# Improving throughput by using tasks

After completing this chapter, you will be able to:

- Describe the benefits of implementing parallel operations in an application.
- Explain the relationship between parallelization and the number of processor cores available.
- Use the Task class and the Parallel class to create and run parallel operations in an application.
- Cancel long-running tasks and handle exceptions raised by parallel operations.

In the bulk of this book, you've learned how to use C# to write programs that run in a single-threaded manner. I mean that at any point in time, a program executes a single instruction. This might not always be the most efficient approach for an application to take, however. If you have the appropriate processing resources available, some applications might run more quickly if you divide them into parallel paths of execution that can run concurrently.

This chapter is concerned with improving throughput in your applications by maximizing the use of available processing power. Specifically, you'll learn how to use Task objects to apply effective multitasking to computationally intensive applications.

# Why perform multitasking by using parallel processing?

There are two primary reasons why you might want to perform multitasking in an application:

- To improve responsiveness A long-running operation might involve tasks that don't require processor time. Common examples include I/O-bound operations such as reading from or writing to a local disk or sending and receiving data across a network. In both of these cases, it doesn't make sense