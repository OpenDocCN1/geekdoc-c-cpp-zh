
as with the namespace, C# allows the omission of the type name from a method call whenever the method is a member of the type containing the call expression. (Examples of method calls such as this appear in Listing 4.4.) The type name is unnecessary in such cases because the compiler infers the type from the location of the call. If the compiler can make no such inference, the name must be provided as part of the method call.

At their core, types are a means of grouping together methods and their associated data. For example, Console is the type that contains the Write(), WriteLine(), and ReadLine() methods (among others). All of these methods are in the same “group” because they belong to the Console type.

## Scope

In the previous chapter you learned that the “scope” of a program element is the region of text in which it can be referred to by its unqualified name. A call that appears inside a type declaration to a method declared in that type does not require the type qualifier because the method is “in scope” throughout its containing type. Similarly, a type is “in scope” throughout the namespace that declares it; therefore, a method call that appears in a type in a particular namespace need not specify that namespace in the method call name.

## Method Name

Every method call contains a method name, which might or might not be qualified with a namespace and type name, as we have discussed. After the method name comes the argument list; the argument list is a parenthesized, comma-separated list of the values that correspond to the parameters of the method.

## Parameters and Arguments

A method can take any number of parameters, and each parameter is of a specific data type. The values that the caller supplies for parameters are called the arguments; every argument must correspond to a particular parameter. For example, the following method call has three arguments:

```
System.IO.File.Copy(
    oldFileName, newFileName, false)
```

will see shortly, these methods specify a return type of void just as the HelloWorld declaration of Main returned void.

## Statement versus Method Call

Listing 4.3 provides a demonstration of the difference between a statement and a method call. Although `System.Console.WriteLine("Hello {0}!", System.Console.ReadLine());` is a single statement, it contains two method calls. A statement often contains one or more expressions, and in this example, two of those expressions are method calls. Therefore, method calls form parts of statements.

Although coding multiple method calls in a single statement often reduces the amount of code, it does not necessarily increase the readability and seldom offers a significant performance advantage. Developers should favor readability over brevity.

> **NOTE**
> 
> In general, developers should favor readability over brevity. Readability is critical to writing code that is self-documenting and, therefore, more maintainable over time.

## Declaring a Method

This section expands on the explanation of declaring a method to include parameters or a return type. Listing 4.4 contains examples of these concepts, and Output 4.1 shows the results.

```
**LISTING 4.4: Declaring a Method**

```csharp
class IntroducingMethods
{
    public static void Main()
    {
        string firstName;
        string lastName;
        string fullName;
        string initials;
```
```

## Chapter 4: Methods and Parameters

```
System.Console.WriteLine("Hey you!");

firstName = GetUserInput("Enter your first name: ");
lastName = GetUserInput("Enter your last name: ");

fullName = GetFullName(firstName, lastName);
initials = GetInitials(firstName, lastName);
DisplayGreeting(fullName, initials);
}

static string GetUserInput(string prompt)
{
    System.Console.Write(prompt);
    return System.Console.ReadLine();
}

static string GetFullName(  // C# 6.0 expression-bodied method
    string firstName, string lastName) =>
        $"{ firstName } { lastName }";

static void DisplayGreeting(string fullName, string initials)
{
    System.Console.WriteLine(
        $"Hello { fullName }! Your initials are { initials }.");
    return;
}

static string GetInitials(string firstName, string lastName)
{
    return $"{ firstName[0] }. { lastName[0] }.";
}
}
```

## OUTPUT 4.1

```
Hey you!
Enter your first name: Inigo
Enter your last name: Montoya
Your full name is Inigo Montoya.
```

Five methods are declared in Listing 4.4. From Main() the code calls GetUserInput(), followed by a call to GetFullName() and GetInitials(). All of the last three methods return a value and take arguments. One declaration, GetFullName(), leverages the C# 6.0 styled expression-bodied method syntax discussed shortly. In addition, the listing calls DisplayGreeting(), which doesn’t return any data. No method in C# can exist outside the confines of an enclosing type; in this case, the enclosing type is the IntroducingMethods class. Even the Main method examined in Chapter 1 must be within a type.

## Language Contrast: C++/Visual Basic—Global Methods

C# provides no global method support; everything must appear within a type declaration. This is why the Main() method was marked as static—the C# equivalent of a C++ global and Visual Basic “shared” method.

## BEGINNER TOPIC

## Refactoring into Methods

Moving a set of statements into a method instead of leaving them inline within a larger method is a form of refactoring. Refactoring reduces code duplication, because you can call the method from multiple places instead of duplicating the code. Refactoring also increases code readability. As part of the coding process, it is a best practice to continually review your code and look for opportunities to refactor. This involves looking for blocks of code that are difficult to understand at a glance and moving them into a method with a name that clearly defines the code’s behavior. This practice is often preferred over commenting a block of code, because the method name serves to describe what the implementation does.

For example, the Main() method that is shown in Listing 4.4 results in the same behavior as does the Main() method that is shown in Listing 1.15 in Chapter 1. Perhaps even more noteworthy is that although both listings are trivial to follow, Listing 4.4 is easier to grasp at a glance by just viewing the Main() method and not worrying about the details of each called method’s implementation.

In earlier versions of Visual Studio, you can select a group of statements, right-click on it, and then select the Extract Method refactoring from the Refactoring section of the context menu to automatically move a group of statements to a new method. In Visual Studio 2015, the refactorings are available from the Quick Actions section of the context menu.

## Formal Parameter Declaration

Consider the declarations of the DisplayGreeting(), GetFullName(), and the GetInitials() methods. The text that appears between the parentheses of a method declaration is the formal parameter list. (As we will see

when we discuss generics, methods may also have a **type parameter list**. When it is clear from context which kind of parameters we are discussing, we will simply refer to them as “parameters” in a “parameter list.” Each parameter in the parameter list includes the type of the parameter along with the parameter name. A comma separates each parameter in the list.

Behaviorally, most parameters are virtually identical to local variables, and the naming convention of parameters follows accordingly. Therefore, parameter names use camelCase. Also, it is not possible to declare a local variable (a variable declared inside a method) with the same name as a parameter of the containing method, because this would create two “local variables” of the same name.

> **Guidelines**
> 
> **DO** use “camelCasing” for parameter names.

## Method Return Type Declaration

In addition to GetUserInput(), GetFullName(), and GetInitials() methods requiring parameters to be specified, each of these methods also includes a **method return type**. You can tell that a method returns a value because a data type appears immediately before the method name in the method declaration. Each of these method examples specifies a `string` return type. Unlike with parameters, of which there can be any number, only one method return type is allowable.

As with GetUserInput() and GetInitials(), methods with a return type almost always contain one or more “return statements” that return control to the caller. A return statement consists of the return keyword followed by an expression that computes the value the method is returning. For example, the GetInitials() method’s return statement is `return $"{ firstName[0] }. { lastName[0] }";`. The expression (an interpolated string in this case) following the return keyword must be compatible with the stated return type of the method.

If a method has a return type, the block of statements that makes up the body of the method must have an “unreachable end point.” That is, there must be no way for control to “fall off the end” of a method without it returning a value. Often the easiest way to ensure that this condition
