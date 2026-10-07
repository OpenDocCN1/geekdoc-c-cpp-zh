# Code Blocks, Scopes, and Declaration Spaces

> > Guidelines
AVVOID omitting braces, except for the simplest of single-line if statements.

Chapter 4: Operators and Control Flow

Code blocks are often referred to as *scopes*, but the two terms are not exactly interchangeable. The *scope* of a named thing is the region of source code in which it is legal to refer to the thing by its unqualified name. The scope of a local variable, for example, is exactly the text of the code block that encloses it, which explains why it is common to refer to code blocks as scopes.

Scopes are often confused with declaration spaces. A **declaration space** is a logical container of named things in which two may not have the same name. A code block defines not only a scope but also a local variable declaration space. It is illegal for two local variables with the same name to appear in the same declaration space. Similarly, it is not possible to declare two methods with the signature of `Main()` within the same class. (This rule is relaxed somewhat for methods: Two methods may have the same name in a declaration space provided that they have different signatures. The signature of a method includes its name and the number and types of its parameters.) Within a block, a local variable can be mentioned by name and must be the unique thing that is declared with that name in the block. Outside declaring the block, there is no way to refer to a local variable by its name; the local variable is to be “out of scope” outside the block.

In summary, C# uses a scope to determine what thing name refers to; a declaration space determines when two things with the same name conflict with each other. In Listing 4.28 (with Output 4.15), declaring the local variable message inside the block statement embedded in the if statement restricts its scope to the block statement only; the local variable is out of scope when its name is used later in the method. To avoid an error, you must declare the variable outside the block.