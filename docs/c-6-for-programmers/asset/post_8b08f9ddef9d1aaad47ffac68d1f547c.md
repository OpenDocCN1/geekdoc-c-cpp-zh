
x squared: 100

**Fig. 7.9 |** Square method used to demonstrate the method-call stack and activation records. (Part 2 of 2.)

First, the operating system calls Main—this pushes an activation record onto the stack (Fig. 7.10). This tells Main how to return to the operating system (i.e., transfer to return address R1) and contains the space for Main’s local variable x, which is initialized to 10.

### Step 1: Operating system calls Main to begin program execution

```csharp
static void Main()
{
    int x = 10;
    Console.WriteLine("x squared: {Square(x)}");
}
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_214_0.png)

**Fig. 7.10 |** Method-call stack after the operating system calls Main to execute the program.

Method Main—before returning to the operating system—calls method Square in line 11 of Fig. 7.9. This causes a stack frame for Square (lines 15–18) to be pushed onto the method-call stack (Fig. 7.11). This stack frame contains the return address that Square needs to return to Main (i.e., R2) and the memory for Square’s local variable y.

After Square performs its calculation, it needs to return to Main—and no longer needs the memory for y. So Square’s stack frame is popped from the stack—giving Square the return location in Main (i.e., R2) and losing Square’s local variable (Step 3). Figure 7.12 shows the method-call stack after Square’s activation record has been popped.

Method Main now displays the result of calling Square (Fig. 7.9, line 11). Reaching the closing right brace of Main causes its stack frame to be popped from the stack, giving Main the address it needs to return to the operating system (i.e., R1 in Fig. 7.10)—at this point, Main’s local variable x no longer exists. You’ve now seen how valuable the stack data structure is in implementing a key mechanism that supports program execution. There’s a significant omission in the sequence of illustrations in this section. See if you can spot it before reading the next sentence. The call to the method Console.WriteLine, of course, also involves the stack, which should be reflected in this section’s illustrations and discussion.

### Step 2: Main calls method Square to perform calculation

```csharp
static void Main()
{
   int x = 10;
   Console.WriteLine(
      "x squared: {Square(x)}");
}
```

```csharp
static int Square(int y)
{
   return y * y;
}
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_215_0.png)

Fig. 7.11 | Method-call stack after Main calls Square to perform the calculation.

### Step 3: Square returns its result to Main

```csharp
static void Main()
{
   int x = 10;
   Console.WriteLine(
      "x squared: {Square(x)}");
}
```

```csharp
static int Square(int y)
{
   return y * y;
}
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_215_1.png)

Fig. 7.12 | Method-call stack after method Square returns to Main.

## 7.12 Method Overloading

Methods of the same name can be declared in the same class, as long as they have different sets of parameters (determined by the number, types and order of the parameters). This is called method overloading. When an overloaded method is called, the C# compiler selects the appropriate method by examining the number, types and order of the arguments in the call. Method overloading is commonly used to create several methods with the same name that perform the same or similar tasks, but on different types or different numbers of arguments. For example, Random method Next (Section 7.8) has overloads that accept different numbers of arguments, and Math method Max has overloads that accept different types of arguments (ints vs. doubles). These find the minimum and maximum, respectively, of two values of each of the numeric simple types. Our next example demonstrates declaring and invoking overloaded methods. You'll see examples of overloaded constructors in Chapter 10.

### 7.12.1 Declaring Overloaded Methods

In class MethodOverload (Fig. 7.13), we include two Square methods—one that calculates the square of an int (and returns an int) and one that calculates the square of a double (and returns a double). Although these methods have the same name and similar parameter lists and bodies, you can think of them simply as different methods. It may help to think of the method names as “Square of int” and “Square of double,” respectively.

```csharp
// Fig. 7.13: MethodOverload.cs
// Overloaded method declarations.
using System;

class MethodOverload
{
   // test overloaded square methods
   static void Main()
   {
      Console.WriteLine("Square of integer 7 is {Square(7)}");
      Console.WriteLine("Square of double 7.5 is {Square(7.5)}");
   }

   // square method with int argument
   static int Square(int intValue)
   {
      Console.WriteLine("Called square with int argument: {intValue}");
      return intValue * intValue;
   }

   // square method with double argument
   static double Square(double doubleValue)
   {
      Console.WriteLine(
         "Called square with double argument: {doubleValue}");
      return doubleValue * doubleValue;
   }
}
```

**Fig. 7.13** | Overloaded method declarations. (Part 1 of 2.)

```
Called square with int argument: 7
Square of integer 7 is 49
Called square with double argument: 7.5
Square of double 7.5 is 56.25
```

Fig. 7.13 | Overloaded method declarations. (Part 2 of 2.)

Line 10 in Main invokes method Square with the argument 7. Literal integer values are treated as type int, so the method call in line 10 invokes the version of Square at lines 15–19 that specifies an int parameter. Similarly, line 11 invokes method Square with the argument 7.5. Literal real-number values are treated as type double, so the method call in line 11 invokes the version of Square at lines 22–27 that specifies a double parameter. Each method first outputs a line of text to prove that the proper method was called in each case.

The overloaded methods in Fig. 7.13 perform the same calculation, but with two different types. C#'s generics feature provides a mechanism for writing a single “generic method” that can perform the same tasks as an entire set of overloaded methods. We discuss generic methods in Chapter 18.

### 7.12.2 Distinguishing Between Overloaded Methods

The compiler distinguishes overloaded methods by their signature—a combination of the method’s name and the number, types and order of its parameters. The signature also includes the way those parameters are passed, which can be modified by the ref and out keywords (discussed in Section 7.18). If the compiler looked only at method names during compilation, the code in Fig. 7.13 would be ambiguous—the compiler could not know how to distinguish between the Square methods (lines 15–19 and 22–27). Internally, the compiler uses signatures to determine whether a class’s methods are unique in that class.

For example, in Fig. 7.13, the compiler will use the method signatures to distinguish between the “Square of int” method (the Square method that specifies an int parameter) and the “Square of double” method (the Square method that specifies a double parameter). As another example, if Method1’s declaration begins as

```
void Method1(int a, float b)
```

then that method will have a different signature than a method that begins with

```
void Method1(float a, int b)
```

The order of the parameter types is important—the compiler considers the preceding two Method1 headers to be distinct.

### 7.12.3 Return Types of Overloaded Methods

In discussing the logical names of methods used by the compiler, we did not mention the methods’ return types. Methods cannot be distinguished by return type. If in a class named MethodOverloadError you define overloaded methods with the following headers:

```
int Square(int x)
double Square(int x)
```

which each have the *same* signature but *different* return types, the compiler generates the following error for the second Square method:

```
Type 'MethodOverloadError' already defines a member called 'Square'
with the same parameter types
```

Overloaded methods can have the *same* or *different* return types if the parameter lists are *different*. Also, overloaded methods need not have the same number of parameters.

> **Common Programming Error 7.9**
>
> Declaring overloaded methods with identical parameter lists is a compilation error regardless of whether the return types are different.

## 7.13 Optional Parameters

Methods can have optional parameters that allow the calling method to *vary the number of arguments* to pass. An optional parameter specifies a default value that’s assigned to the parameter if the optional argument is omitted. You can create methods with one or more optional parameters. *All optional parameters must be placed to the right of the method’s non-optional parameters*—that is, at the end of the parameter list.

> **Common Programming Error 7.10**
>
> Declaring a non-optional parameter to the right of an optional one is a compilation error.

When a parameter has a default value, the caller has the *option* of passing that particular argument. For example, the method header

```
static int Power(int baseValue, int exponentValue = 2)
```

specifies an optional second parameter. Each call to Power must pass at least a baseValue argument, or a compilation error occurs. Optionally, a second argument (for the exponentValue parameter) can be passed to Power. Each optional parameter must specify a default value by using an equal (=) sign followed by the value. For example, the header for Power sets 2 as exponentValue’s default value. Consider the following calls to Power:

- Power()—This call generates a compilation error because this method requires a minimum of one argument.
- Power(10)—This call is valid because one argument (10) is being passed. The optional exponentValue is not specified in the method call, so the compiler uses 2 for the exponentValue, as specified in the method header.
- Power(10, 3)—This call is also valid because 10 is passed as the required argument and 3 is passed as the optional argument.

Figure 7.14 demonstrates an optional parameter. The program calculates the result of raising a base value to an exponent. Method Power (lines 15–25) specifies that its second parameter is optional. In Main, lines 10–11 call method Power. Line 10 calls the method without the optional second argument. In this case, the compiler provides the second argument, 2, using the default value of the optional argument, which is not visible to you in the call.
