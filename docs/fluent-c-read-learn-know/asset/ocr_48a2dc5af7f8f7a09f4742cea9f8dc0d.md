# DIRECTIVES

Although Task List and XML comments are understood by Visual Studio, all comments are ignored by the compiler. That doesn't mean you can't give the compiler directions, however. The C# compiler understands a small set of DIRECTIVES that you can use to control what code it includes in the output. ATTRIBUTES, on the other hand, are included in the final output, and used to describe a code object.

# LANGUAGE ELEMENTS

DIRECTIVES

STATEMENTS

COMMENTS

Directives are often used in conjunction with build configuration to control the code output.

DIRECTIVES

ATTRIBUTES

Attributes describe a code object to the CLR. They're like directives in many ways, but we won't be discussing them until you have a few more concepts under your belt.

> **WORDS FOR THE WISE**
> 
> In computer science, a preprocessor is a program that prepares input for another program. In older languages, directives were handled by a preprocessor that parsed them before passing the source code onto the compiler proper. C# doesn't use a preprocessor, but directives are still usually called preprocessor directives, even in the Microsoft documentation.