# Declaring method

The syntax for declaring a C# method is as follows:

Click here to view code image

```
returnType methodName( parameterList )
{
    // method body statements go here
}
```

The following is a description of the elements that make up a declaration:

+   - The returnType is the name of a type and specifies the kind of information the method returns as a result of its processing. This can be any type, such as int or string. If you are writing a method that does not return a value, you must use the keyword void in place of the return type.
- The methodName is the name used to call the method. Method names follow the same identifier rules as variable names, whereas addValues is not. For now, you should follow the camelCase convention for method names—for example, displayCustomer.
- The parameterList is optional and describes the types and names of the information that you can pass into a method for it to process. You write declaring variables, with the name of the type followed by opening and closing parentheses, ( ), as though you're declaring variables, with the name of the parameter. If you are writing two or more parameters, you must separate them with commas.
- The method body statements are the lines of code that run when the method is called. They are enclosed between opening and closing braces, { }.

> Important If you program in C, C++, or Visual Basic, you should note that C# does not support global methods. You must write all your methods inside a class; otherwise, your code will not compile.

Here’s the definition of a method called addValues that returns an int result and has two int parameters, leftHandSide and rightSide: