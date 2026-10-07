
## Declaring a Method

execution time, the Console.ReadLine() method executes first, and its return value is passed directly into the Console.WriteLine() method, rather than into a variable.

Not all methods return data. Both versions of Console.Write() and Console.WriteLine() are examples of such methods. As you will see shortly, these methods specify a return type of void, just as the HelloWorld declaration of Main returned void.

# Statement versus Method Call

Listing 5.3 provides a demonstration of the difference between a statement and a method call. Although Console.WriteLine($"{Hello {System.ReadLine()}"); is a single statement, it contains two method calls. A statement often contains one or more expressions, and in this example, two of those expressions are method calls. Therefore, method calls form parts of statements.

Although coding method calls in a single statement reduces the amount of code, it does not necessarily increase the readability and seldom offers a significant performance advantage. Developers should favor readability over brevity.

> NOTE
in general, developers should favor readability over brevity. Readability is critical to writing code that is self-documenting and therefore maintainable over time.

# Declaring a Method

This section expands the explanation of declaring a method to include parameters or a return type. Listing 5.4 contains examples of these concepts, and Output 5.1 shows the results.

Listing 5.4: Declaring a Method

```
public class IntroducingMethods{
    public static void Main()
```

```
{
  string firstName;
  string lastName;
  string fullName;
  string initials;

  Console.WriteLine("Hey you!");

  firstName = GetUserInput("Enter your first name: ");
  lastName = GetUserInput("Enter your last name: ");

  fullName = GetFullName(firstName, lastName);
  initials = GetInitials(firstName, lastName);
  DisplayGreeting(fullName, initials);
}
```

```
static string GetUserInput(string prompt)
{
  Console.Write(prompt);
  return Console.ReadLine() ?? string.Empty;
}
```

# OUTPUT 5.1

Hey you!
Enter your first name: Inigo

# Declaring a Method

Enter your last name: Montoya
Hello Inigo Montoya! Your initials are I. M.

Listing 5.4 declares five methods. From Main() the code calls
GetUserInput(), followed by a call to GetFullName() and GetInitials().
All of the last three methods return a value and take arguments. In addition, the
listing calls DisplayGreeting(), which doesn't return any data.

# Language Contrast: C++/Visual Basic—Global Methods

C# provides no global method support; everything must appear within a type
declaration. This is why the Main() method was marked as static—the C# equivalent of a C++ global and Visual Basic "shared" method. The statements
that appear independent from a method and the methods that appear
independently from a class are even conforming to this rule because the C#
compiler generates the surrounding method and class for these seemingly
independent constructs. For more information, see "Top-Level Statements" later
in this chapter.

# BEGINNER TOPIC

# Refactoring into Methods

Moving a set of statements into a method instead of leaving them inline within a
larger method is a form of refactoring. Refactoring reduces code duplication,
because you can call the method from multiple places instead of duplicating the
code. Refactoring also increases code readability. As part of the coding process, it is
best practice to continually review your code and look for opportunities to refactor.
This involves looking for blocks of code that are difficult to understand at a glance
and moving them into a method with a name that clearly defines the code's behavior.
This practice is often preferred over added comments to a block of code, because the
method name serves to describe what the implementation does. Listing 5.4 is easy to
grasp at a glance by just viewing the Main() method and not worrying about the
details of each called method's implementation.

Visual Studio allows you to right-click on a block of code within a method and click Quick Actions and Refactorings... (Ctrl+.) to extract the block into its own method, automatically inserting code to call the new method from the original location.

# Formal Parameter Declaration

Consider the declarations of the DisplayGreeting(), GetFullName(), and the GetInitials() methods. The text that appears between parentheses of a method declaration is the formal parameter list. (As we will see when we discuss generics, methods may also have a type parameter list. When it is clear from the context which kind of parameters we are discussing, simply refer to them as parameters in a parameter list.) Each parameter in the parameter list includes the type of the parameter along with the parameter name. A comma separates each parameter in the list.

Behaviorally, most parameters are virtually identical to local variables, and the naming convention of parameters follows accordingly. Therefore, parameter names use camelCase. Also, it is not possible to declare a local variable (a variable declared inside a method) with the same name as a parameter of the containing method, because this would create two local variables of the same name.

> Guidelines
DO use camelCasing for parameter names.

# Method Return Type Declaration

In addition to GetUserInput(), GetFullName(), and the GetInitials() each of these methods includes a method return type to be specified, You can tell that a method returns a value because a data type appears immediately before the method name in the method declaration. Each of these method examples specifies a string return type. Unlike parameters, of which there can be any number, only one return type is allowable.

# Declaring a Method 229

As with GetUserInput() and GetInitials(), methods with a return type almost always contain one or more return statements that return control to the caller. A return statement consists of the return keyword followed by the expression that computes the value the method is returning. For example, the GetInitials() method's return statement is `return ${firstName[0]}. {lastName[0]}`. The expression (an interpolated string in this case) following the return keyword must be compatible with the stated return type of the method.

If a method has a return type, the block of statements that makes up the body of the method must not have an unreachable end. That is, there must be no way for control "fall off the end" of a method without returning a value. Often the easiest way to ensure that this condition is met is to make the last statement of the method a return statement. However, return statements can appear in locations other than the end of a method implementation. For example, an if or switch statement in a method implementation could include a return statement within it; see Listing 5.5 for an example.

- Listing 5.5: A return Statement before the End of the Method

```
public class Program {
    // ...

    public static bool MyMethod() {
        string command = ObtainCommand();
        switch(command) {
            case "quit":
                return false;
                // omitted, other cases
            default:
                return true;
        }
    }
}
```

2. For example, you could throw an exception instead.

# Chapter 5: Parameters and Methods

```
// ...
}
```

(Note that a return statement transfers control out of the switch, so no break statement is required to prevent fall-through in a switch.)

In Listing 5.5, the last statement in the method is not a return statement; it is a switch statement. However, the compiler can deduce that every possible code path through the method results in a return, so that the end point of the method is not reachable. Thus, this method is legal even though it does not end with a return statement.

If particular code paths include unreachable statements following the return, the compiler will issue a warning that indicates the additional statements will never execute.

Though C# allows a method to have multiple return statements, code is generally more readable and easier to maintain if there is a single exit location than multiple returns sprinkled through various code paths of the method.

Specifying void as a return type indicates that there is no return value from the method. As a result, a call to the method may not be assigned to a variable or used as a parameter type at the call site. A void method may be called only as a statement. Furthermore, within the body of the method the return statement becomes optional, and when it is specified, there must be no value following the return keyword. For example, the return of Main() in Listing 5.4 is void, and there is no return statement in the method. However, DisplayGreeting() includes an (optional) return statement that is not followed by any returned result.

Although, technically, a method can have only one return type, the return type could be a tuple. As a result, starting with C# 7.0, it is possible to return multiple values packaged as a tuple using C# tuple syntax. For example, you could declare a GetName() method, as shown in Listing 5.6.

# Listing 5.6: Returning Multiple Values Using a Tuple

```
public class Program{
    static string GetUserInput(string prompt)
```
