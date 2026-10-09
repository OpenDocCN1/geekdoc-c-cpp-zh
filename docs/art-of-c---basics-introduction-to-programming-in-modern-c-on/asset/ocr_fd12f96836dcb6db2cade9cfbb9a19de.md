# # Review - C# Key Concepts

We covered a lot of ground in Part I. Here's a list of some of the topics we went through. These are meant to be reminders rather than the real summaries.

If any of the concepts listed here are not very clear to you, then you can go back and review the example code and the lessons again. Or, you can refer to other references for more information.

# # C# Program Structure

# ## Main Method and Top Level Statements

A C# program can be built into an executable or a library. An executable C# program must include one and only Main() method, as an entry point to the program.

The "top level statements" can be used in lieu of the Main() method. The top level statements are automatically converted to a Main method of an implicitly created class by the compiler. The top level static methods are also converted into static methods of that class.

# ## Namespace

We can use short forms of the names from other namespaces using the `using` or `using static` declarations. Namespaces are primarily used in C# to organize "names" into groups and to minimize the chance of name collisions across different C# programs and libraries. As of C# 10.0, certain namespaces like `System` are implicitly imported and we do not need to use explicit qualifications for the names from those namespaces even without using the `using` declarations.