# Understanding Storage Duration and Scope

All variables have a finite lifetime when your program executes. They come into existence from the point at which you declare them and then, at some point, they disappear — at the latest, when your program terminates. How long a particular variable lasts is determined by a property called its storage duration. There are three different kinds of storage duration that a variable can have:

+   - Automatic storage duration
+   - Static storage duration
+   - Dynamic storage duration

Which of these a variable will have depends on how you create it. I will defer discussion of variables with dynamic storage duration until Chapter 4, but you will be exploring the characteristics of the other two in this chapter.

Another property that variables have is scope. The scope of a variable is simply that part of your program over which the variable name is valid. Within a variable’s scope, you can legally refer to it, to set its value or use it in an expression. Outside of the scope of a variable, you cannot refer to its name — any attempt to do so will cause a compiler error. Note that a variable may still exist outside of its scope, even though you cannot refer to it by name. You will see examples of this situation a little later in this discussion.

All of the variables that you have declared up to now have had automatic storage duration, and are therefore called automatic variables. Let’s take a closer look at these first.

# Automatic Variables

The variables that you have declared so far have been declared within a block — that is, within the extent of a pair of braces. These are called automatic variables and are said to have local scope or block scope. An automatic variable is “in scope” from the point at which it is declared until the end of the block containing its declaration. The space that an automatic variable occupies is allocated automatically in a memory area called the stack that is set aside specifically for this purpose. The default size for the stack is 1MB, which is adequate for most purposes, but if it should turn out to be insufficient, you can increase the size of the stack by setting the /STACK option for the project to a value of your choosing.

An automatic variable is “born” when it is defined and space for it is allocated on the stack, and it automatically ceases to exist at the end of the block containing the definition of the variable. This will be at the closing brace matching the first opening brace that precedes the declaration of the variable. Every time the block of statements containing a declaration for an automatic variable is executed, the variable is created anew, and if you specified an initial value for the automatic variable, it will be reinitialized each time it is created. When an automatic variable dies, its memory on the stack will be freed for use by other automatic variables

There is a keyword, auto, which you can use to specify automatic variables, but it is rarely used since it is implied by default. What follows is an example of what I’ve discussed so far about scope.