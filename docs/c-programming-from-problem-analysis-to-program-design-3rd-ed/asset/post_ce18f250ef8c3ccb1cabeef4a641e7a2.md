
## Access Modifiers

Another type of modifier is an access modifier. It specifies the level of accessibility for types and their members. C# includes the following accessibility modifiers:

- `public`
- `protected`
- `internal`
- `protected internal`
- `private`

Public access offers the fewest access limitations; there are basically no restrictions on accessing `public` members or classes. Notice in Example 3-1 that the `class` definition and the `Main( )` method heading include the `public` access modifier. By specifying a `public` access, other classes can reuse your classes in different applications.

Private is the most restrictive access modifier. Private members are accessible only within the body of the `class` in which they are declared. Often in object-oriented design, data is defined with a `private` modifier and methods that access the data are declared to have `public` access. By defining the data members as `private`, you restrict access to the data through the members' methods or properties that you learn about in this chapter.

Table 3-1 shows the different accessibility levels of access modifiers.

Table 3-1 C# access modifiers

| Modifiers | Explanation of accessibility |
| --- | --- |
| `public` | No restrictions |
| `protected` | Limited to the containing *class* or classes derived from the containing *class* |
| `internal` | Limited to current project |
| `protected internal` | Limited to current project or classes derived from *class* |
| `private` | Limited to containing *class* |

When a `class` or a `class` member does not specify a modifier, the default accessibility level of `private` is assumed. Later in this chapter, you will read about one other type of modifier: `override`. This keyword is added to the heading of a method to declare a new definition for a previously defined method. Both the previously defined method and the new one are referenced by the same identifier.

## Return Type

The return type identifies what type of value is returned when the method is completed. Any of the predefined or valid user-defined types can be returned. Methods can return a value when all the statements of the method are complete, or they can simply return control to the method that called them, without bringing a value back.

The return type is always listed immediately preceding the name of the method, as shown in Figure 3-1. Methods do not have to return anything; however, they can return at most one data type through the method's name.

> You will learn about arrays and collections such as ArrayLists in Chapter 7. C# allows a method to return a collection; however, the return must be through a single identifier. That identifier can be the name of an array.

If a method does not return a value, the void keyword is placed at the return type location in the method heading, as shown in the following line of code:

```
public void DisplayInstructions( )
```

If a return type other than void is specified in the method heading, there must be a return statement included in the body of the method. The value returned must be a compatible value—one that either matches the type in the heading or can be stored in that type.

The return statement takes the form:

```
return [value];
```

Note that value is enclosed in square brackets to indicate that it is optional. If the method heading uses void as the return type, the return statement can be omitted or included as follows:

```
return;
```

Whenever the return type is not void, you must have a return value following the return keyword. This value can be a literal, arithmetic expression, or variable that holds a value. Example 3-3 illustrates returning a calculated value.

### Example 3-3

```
public static double CalculateMilesPerGallon
    (int milesTraveled, double gallonsUsed)
{
    return milesTraveled / gallonsUsed;
}
```

The method heading in Example 3–3 indicates that a **double** value is returned. This is the **double** that follows the **public** keyword. Inside the body of the method, the result of the division produces a compatible **double** value.

The value being returned is sent back to the location in the program that called the method. For example, the value returned from the `CalculateMilesPerGallon( )` method is sent back to the `WriteLine( )` method for display in the call that follows:

```
Console.WriteLine("Miles per gallon = {0:N2}",
                  CalculateMilesPerGallon(289, 12.2));
```

The output produced from the `WriteLine( )` method would be:

```
Miles per gallon = 23.69
```

![](img/e33ae760e23d89eac66541252ad65de8_165_0.png)

Your programs are easier to modify and debug if your methods have one entry and one exit. This is a problem-solving technique you should try to include in your design. The implication is that you should try to have only one **return** statement in a method.

## Method Name

When naming a method, you follow the rules for creating an identifier, which were described in Chapter 2. Identifiers should be meaningful names that label the overall purpose of the segment of code. Many programmers use the standard convention of naming the method with an action verb phrase. This verb phrase should describe what the method is intending to accomplish. **Pascal case style** is used for **class** and method identifiers. This C# convention specifies that the first character is uppercase when the identifier has at least three characters. Subsequent words that are part of the identifier also begin with an uppercase character. Examples of method identifiers following these style conventions include: `CalculateSalesTax( )`, `AssignSectionNumber( )`, `DisplayResults( )`, `InputAge( )`, and `ConvertInputValue( ).`

![](img/e33ae760e23d89eac66541252ad65de8_165_1.png)

C# programs use the **Camel case style** convention for data member identifiers. This style specifies that the first letter of identifiers is lowercase and the first letter of each subsequent concatenated word is capitalized. Examples are `studentName`, `major`, and `yearInSchool`.

## Parameters

The items inside the parentheses of the method heading are called the parameters, or arguments. Sometimes a method requires the supply of unique data. For example, if a method is written to calculate the average of three values, the method requires that these three values be sent to it. The `CalculateMilesPerGallon( )` method in Example 3–3 required two arguments: an **int** value for `milesTraveled` and a **double** value for `gallonsUsed`. It is through parameters and arguments that the data can be sent into a method.

When writing a method, you decide what type of unique data is needed for the method. You then place the data type and an identifier for the data type inside the parentheses. You must include matched pairs of types and identifiers inside the parentheses. The two matched pairs of parameters for the `CalculateMilesPerGallon( )` method are as follows:

```
(int milesTraveled, double gallonsUsed)
```

In the body of the method, the identifiers are used to reference where and when the unique data item should be used. For the `CalculateMilesPerGallon( )` method, `milesTraveled` and `gallonsUsed` were used in an arithmetic expression. The result of the expression is returned to the calling method.

Some programmers make a distinction between parameters and arguments, using the term **parameter** to refer to items appearing in the heading of the method and **argument** for the items appearing in the call to the method. Others make a distinction between arguments and parameters by adding actual and formal onto the terms. **Formal parameters**, or arguments, appear in the heading of a method. **Actual arguments**, or parameters, appear in the call. Think of the actual argument as being the actual data that is sent to the method. The formal parameters are like placeholders; they formally indicate what type of data is expected to be sent for the method to use. This book uses the term "parameters" to refer to the items in the method heading and the term "arguments" for items sent into the method via a method call. For Example 3-3, the arguments for the `CalculateMilesPerGallon( )` method are 289 and 12.2. This is actual data or numbers; however, the actual argument could be an identifier for a variable. It could be an expression involving an arithmetic statement or a call to another method.

Like `return` types, parameters are optional. If no parameters are included, an open and closed parenthesis is used. If more than one parameter is included, they are separated by a comma.

> Some languages place the `void` keyword inside the parentheses in place of the parameter list to indicate that no parameters are needed. C# does not allow this and generates a syntax error.

There are several different types of parameters, which are explored later in this chapter.

## Method Body

As you saw in Example 3-1, statements making up the body are enclosed in curly braces. The body for the following `DisplayMessage( )` method consists of two calls to the `Write( )` method in the `Console` class, one call to the `WriteLine( )` method in the `Console` class, and a `return` statement that does not return a value.

```csharp
public void DisplayMessage( )
{
    Console.Write("This is ");
    Console.Write("an example of a method ");
    Console.WriteLine("body. ");
    return;    // no value is returned
}
```
