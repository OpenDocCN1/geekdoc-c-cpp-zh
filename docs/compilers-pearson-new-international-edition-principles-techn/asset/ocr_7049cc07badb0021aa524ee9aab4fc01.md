# # 1.6. PROGRAMMING LANGUAGE BASICS

# ## Procedures, Functions, and Methods

To avoid saying “procedures, functions, or methods,” each time we want to talk about a subprogram that may be called, we shall usually refer to all of them as “procedures.” The exception is that when talking explicitly of programs in languages like C that have only functions, we shall refer to them as “functions.” Or, if we are discussing a language like Java that has only methods, we shall use that term instead.

A function generally returns a value of some type (the “return type”), while a procedure does not return any value. C and similar languages, which have only functions, treat procedures as functions that have a special return type “void,” to signify no return value. Object-oriented languages like Java and C++ use the term “methods.” These can behave like either functions or procedures, but are associated with a particular class.

+   3. The scope of a top-level declaration of a name *x* consists of the entire program that follows, with the exception of those statements that lie within a function that also has a declaration of *x*.

The additional detail regarding the C static-scope policy deals with variable declarations within statements. We examine such declarations next and in Example 1.6. □

In C, the syntax of blocks is given by

+   1. One type of statement is a block. Blocks can appear anywhere that other types of statements, such as assignment statements, can appear.
+   2. A block is a sequence of declarations followed by a sequence of statements, all surrounded by braces.

Note that this syntax allows blocks to be nested inside each other. This nesting property is referred to as *block structure*. The C family of languages has block structure, except that a function may not be defined inside another function.

We say that a declaration *D* “belongs” to a block *B* if *B* is the most closely nested block containing *D*; that is, *D* is located within *B*, but not within any block that is nested within *B*.

The static-scope rule for variable declarations in block-structured languages is as follows. If declaration *D* of name *x* belongs to block *B*, then the scope of *D* is all of *B*, except for any blocks *B'* nested to any depth within *B*, in which *x* is redeclared. Here, *x* is redeclared in *B'* if some other declaration *D'* of the same name *x* belongs to *B'*.