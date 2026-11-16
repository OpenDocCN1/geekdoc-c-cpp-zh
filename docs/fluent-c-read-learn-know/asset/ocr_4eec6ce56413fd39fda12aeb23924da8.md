# DECLARING ELEMENTS

With a very few exceptions, everything you do in C# is a statement or part of a statement. To create a declared element, you use a particular kind of statement called a declaration statement. (No surprise there, right?)

We'll talk about modifiers in Chapter 8.

C# is case-sensitive. You have to use the word "const", not "Const" or "CONST".

The name of the element is the word you'll use to refer to it in your code. It's called an IDENTIFIER, and we'll look at the rules for creating one in a few pages.

```
[modifier] [const] <type> <name> [= <value>];
private const Elephant dumbo = new Elephant();
```

The keyword const tells the compiler that the element is a CONSTANT and its value will never change. You must provide the value of the constant when you declare it.

The type specifier tells the compiler whether your element will hold a goldfish or an elephant (or an Int32).

You can set an initial value for your element (you have to do it for a constant) using this syntax.

Don't forget the semicolon!

> MAKE A NOTE
> There's a convention for syntax diagrams, and I'm using it here. Anything in square brackets, like [modifier], is optional. Anything in angle brackets, like <type> is a placeholder that you'll need to replace with an actual value.