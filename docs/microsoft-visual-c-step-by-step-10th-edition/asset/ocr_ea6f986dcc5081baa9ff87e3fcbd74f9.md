# Chapter 3

# Writing methods and applying scope

After completing this chapter, you will be able to:

+   - Declare methods, pass information to a method, and return information from a method.
- Call methods.
- Define local and class scope.
- Use the debugger to step into and out of methods as they run.
- Use optional parameters and named arguments with methods.

In Chapter 2, “Working with variables, operators, and expressions,” you learned how to declare variables, how to create expressions using operators, and how precedence and associativity control the way in which expressions containing multiple operators are evaluated. In this chapter, you'll learn about methods. You'll see how to declare and call methods, how to use arguments and parameters to pass information to a method, and how to return information from a method using a return statement. You'll also see how to step into and out of methods using the Microsoft Visual Studio 2022 integrated debugger. This information is useful when you need to trace the execution of your methods because they do not work quite as you expect. Finally, you'll learn how to declare methods that take optional parameters and how to invoke methods using named arguments.

# Creating methods

A method is a named sequence of statements. If you have programmed previously using a language such as C, C++, or Microsoft Visual Basic, you will see that a method is similar to a function or subroutine.

A method has a name and a body. The method name should be a meaningful identifier that indicates the overall purpose of the method (calculateIncomeTax, for example). The method body contains the actual statements to be run when the method is called. Additionally, methods can be given some data for processing and can return information, which is usually the result of the processing. Methods are a fundamental and powerful mechanism.