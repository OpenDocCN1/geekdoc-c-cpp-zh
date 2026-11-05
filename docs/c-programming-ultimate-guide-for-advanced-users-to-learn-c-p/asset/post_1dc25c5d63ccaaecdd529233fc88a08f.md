
In C#, literals refer to fixed values that are represented in their understandable form. For example, the number 100 is a literal. Generally, literals and their use are so intuitive that they have been used in some form by all the first example programs. Now the time has come to clarify them formally.

C# literals can be of any of the value types. The manner in which each literal is represented depends upon its type. As explained before, character literals are enclosed between single quotes. For example, 'a' and '%' are both character literals. Integer literals are indicated as numbers without fractional parts. For instance, 10 and -100 are integer literals. Floating-point literals require the use of the decimal point followed by the number's fractional part. For instance, 11.123 is a floating-point literal. C# also enables you to use scientific notation for floating-point numbers. Since C# is a strongly typed language, literals, as well, have a type. Naturally, this raises the following question: What is the type of a numeric literal? For instance, what is the type of 12, 123987, or 0.23? Luckily, C# defines some simple-to-follow rules that answer these questions. First, for integer literals, the type of the literal is the smallest integer type that will hold it, starting with int. Consequently, an integer literal is of type int, uint, long, or ulong, depending on its value. Second, floating-point literals are of type double.

If C#'s default type isn't what you want for a literal, you can explicitly specify its type by adding a suffix. To specify a long literal, add an l or an L. For instance, 12 is an int, but 12L is a long. To indicate an unsigned integer value, affix a u or U. In this manner, 100 is an int, but 100U is a uint. To indicate an unsigned long integer, use ul or UL. For instance, 984375UL is of type ulong.

To specify a float literal, affix an F or f. For instance, 10.19F is of type float. Although redundant, you can indicate a double literal by appending a D or d. (As just mentioned, floating-point literals are double by default.) To specify a decimal literal, follow its value with an m or M. For instance, 9.95M is a decimal literal.

Although integer literals create an int, uint, long, or ulong value by default, they can still be assigned to variables of type byte, sbyte, short, or ushort as long as the value being assigned can be represented by the target type.

### Hexadecimal Literals

In programming, it is sometimes simpler to use a number system based on 16 rather than 10. The base-16 number system is called hexadecimal and uses the digits 0 through 9, plus the letters A through F, which represent 10, 11, 12, 13, 14, and 15. For instance, the hexadecimal number 10 is 16 in decimal. Due to the frequency with which hexadecimal numbers are used, C# enables you to specify integer literals in hexadecimal form. A hexadecimal literal must start with 0x (a zero followed by an x).

### Character Escape Sequences

Enclosing character constants in single quotes works for most printing characters, but a few characters, such as the carriage return, present a special problem when a text editor is used. In addition, certain other characters, such as single and double quotes, have special significance in C#, so you can't use them directly. Thus, C# provides unique escape sequences.

Notice how the `\n` escape sequence is used to produce a new line. You don't have to use multiple WriteLine( ) statements to get multiline output. Simply embed `\n` inside a longer string at the points at which you want the newlines to occur.

In addition to the type of string literal just described, you can specify a verbatim string literal. A verbatim string literal starts with an @, which is followed by a quoted string. The contents of the quoted string are accepted without modification and can span two or more lines. Accordingly, you can include newlines, tabs, etc., but you don't have to use the escape sequences. The only exception is that to get a double quote (`"`), you must use two double quotes in succession (`""`). Here is a program that shows verbatim string literals. The significant point to see about the preceding program is that the verbatim string literals are shown precisely as they are entered into the program. The benefit of verbatim string literals is that you can specify output in your program precisely as it will appear on the screen. However, in the case of multiline strings, the wrapping will make the spacing of your program be obscured. Therefore, the programs in this book will use verbatim string literals. All things considered, they are still a great advantage for some formatting circumstances.

```
// Demonstrate verbatim literal strings.
using System;

class Verbatim {
    static void Main() {
        Console.WriteLine(@"This is a verbatim
string literal
that spans several lines.");
        Console.WriteLine(@"Here is some tabbed output:
1 2 3 4
5 6 7 8
");
        Console.WriteLine(@"Programmers say, ""I like C#.""");
    }
}
```

Variables were presented in Chapter 1. As you learned, variables are declared using this form of declaration:

```
type var-name;
```

where type is the data type of the variable and var-name is its name. You can declare a variable of any valid type, including the value types just described. It is essential to understand that the capabilities of the variable are controlled by its type. For instance, a variable of type bool can't be used to store floating-point values. Moreover, the type of a variable can't change during its lifetime. An int variable can't transform into a char variable, for instance. All variables in C# must be declared. This is fundamental because the compiler must know what the type of a variable is. Consequently, the type of a variable can't be changed during the execution of the program.

Implicitly typed variables were added to C# to deal with some special-case situations, the most significant of which relate to LINQ (Language-Integrated Query), which is described later in this book. For most variables, you should use explicitly typed variables because they make your code easier to read and clearer. Implicitly typed variables should be used only when necessary. They are not intended to replace ordinary variable declarations in general. Generally, use, but don't abuse, this new C# feature. One final point: Only one implicitly typed variable can be declared at any one time.

### Variable Scope

Up until this point, all of the variables that we have been using have been declared at the beginning of the Main( ) method. However, C# enables a local variable to be declared inside any block. As explained in Section 1, a block is started with an opening curly brace and finished with a closing curly brace.

A block defines a scope. In this way, each time you start another block, you are creating another scope. A scope determines what names are visible to different parts of your program. It additionally determines the lifetime of local variables. The most significant scopes in C# are those defined by a class and those defined by a method. A discussion of class scope (and variables declared inside it) is deferred until later in this book, when classes are described. For the time being, we will analyze just the scopes defined by or inside a method.

The scope defined by a method starts with its opening curly brace and finishes with its closing curly brace. However, if that method has parameters, they, too, are incorporated inside the scope defined by the method. As a rule, local variables declared inside a scope are not visible to code that is defined outside that scope. Accordingly, when you declare a variable inside
