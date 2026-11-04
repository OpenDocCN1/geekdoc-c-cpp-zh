Unfortunately, it's easy to forget to call Dispose. To help you remember, C# provides the using statement. The using statement is followed by the object that it manages and, when the using block ends, the program automatically calls the object's Dispose method.

The usual syntax for a using block is:

```
using (variableInitialization)
{
    ... Statements ...
}
```

In this syntax, the variableInitialization declares and initializes the variable that the block controls. (You can declare the object outside of the using block, but putting it inside the block usually makes it easier to read and restricts its scope to the block.)

For example, the following code creates a Graphics object named gr associated with the bitmap bigBitmap. The using block ensures that the program executes the gr object's Dispose method when it finishes the block.

```
using (Graphics gr = Graphics.FromImage(bigBitmap))
{
    // Draw stuff...
}
```

Note that the object's Dispose method is called even if the program exits from the block because of an exception, a return statement, or some other method.

# INVOKING OTHER CONSTRUCTORS

You can give a class many different constructors as long as they have different parameter lists (so C# can tell them apart). For example, you might give the Person class a parameterless constructor, a second constructor that takes first name and last name as parameters, and a third constructor that takes first and last name, street, city, state, and ZIP code as parameters.

Often when you give a class multiple constructors, some of them perform the same actions. In the Person example, the constructor that initializes first name, last name, street, city, state, and ZIP code probably does the same things that the second constructor does to initialize just first and last name.

You can also find overlapping constructor functionality when one class inherits from another. For example, suppose the Person class has FirstName and LastName properties. The Employee class inherits from Person and adds some other properties such as EmployeeId and MailStop. The Person class's constructor initializes the FirstName and LastName properties, something that the Employee class's constructors should also do.

Having several methods perform the same tasks makes debugging and maintaining code harder. Fortunately, C# provides a way you can make one constructor invoke another.

To make one constructor invoke another in the same class, follow the constructor's parameter declarations with a colon and the keyword this, passing this any parameters that the other constructor should receive. For example, the following code shows three constructors for the Person class that invoke each other. The code that invokes other constructors is shown in bold: