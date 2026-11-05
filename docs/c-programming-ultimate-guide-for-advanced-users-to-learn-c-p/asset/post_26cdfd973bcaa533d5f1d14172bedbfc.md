
Notwithstanding the type of string literal simply depicted, you can determine a verbatim string literal. A verbatim string literal starts with a @, which is followed by a quoted string. The contents of the quoted string are accepted without alteration and can span at least two lines. Accordingly, you can incorporate newlines, tabs, etc., however you don't have to use the escape sequences. The main special case is that to get a double quote ("), you should use two double quotes in succession (""). Here is a program that shows verbatim string literals. The significant point to see about the former program is that the verbatim string literals are shown exactly as they are entered into the program. The benefit of verbatim string literals is that you can indicate output in your program precisely as it will show up on the screen. In any case, on account of multiline strings, the wrapping will make the shape of your program be obscured. Therefore, the programs in this book will use verbatim string literals. All things considered, they are still a brilliant advantage for some formatting situations.

```csharp
// Demonstrate verbatim literal strings.
using System;
class Verbatim {
    static void Main() {
        Console.WriteLine(@"This is a verbatim
string literal
that spans several lines.
");
        Console.WriteLine(@"Here is some tabbed output:
1 2 3 4
5 6 7 8
");
        Console.WriteLine(@"Programmers say, ""I like C#.""");
    }
}
```

Variables were presented in Chapter 1. As you learned, variables are declared utilizing this form of declaration:

```text
type var-name;
```

where type is the data type of the variable and var-name is its name. You can declare a variable of any valid type, including the value types just described. It is essential to understand that the capabilities of the variable are controlled by its type. For instance, a variable of type bool can't be used to store floating-point values. Moreover, the type of a variable can't change during its lifetime. An int variable can't transform into a char variable, for instance. All variables in C# must be declared. This is fundamental because the compiler must know what kind of information a variable contains before it can appropriately compile any statement that uses the variable. It likewise empowers C# to perform strict type checking. C# characterizes a few various types of variables. The types that we have been using are called local variables since they are declared inside a method. Note: You should not mistake strings for characters. A character literal represents a single letter of type char. A string containing just one letter is still a string. Despite the fact that strings consist of characters, they are not the same kind.

## Initializing Variable

One approach to give a variable a value is through an assignment statement, as you have already seen. Another route is by giving it an initial value when it is declared. To do this, follow the variable's name with an equal sign and the value being assigned. The general form of initialization is shown here:

```text
type var-name = value;
```

Here, value is the value that is assigned to var-name when var-name is created. The value must be compatible with the specified type. Although the first examples have used only constants as initializers, C# permits variables to be initialized dynamically, using any expression valid at the time when the variable is declared.

As clarified, in C# all variables must be declared. Regularly, a declaration incorporates the type of the variable, for example, int or bool, followed by the name of the variable. In any case, starting with C# 3.0, it is possible to let the compiler determine the type of a variable based on the value used to initialize it. This is called an implicitly typed variable. An implicitly typed variable is declared using the keyword var, and it must be initialized.

The compiler uses the type of the initializer to determine the type of the variable. This assignment is invalid since range is of type int. In this way, it can't be assigned a floating-point value. The main distinction between an implicitly typed variable and an "ordinary" explicitly typed variable is the way the type is resolved. When that type has been resolved, the variable has a type, and this type is fixed all through the lifetime of the variable. Consequently, the type of span can't be changed during the execution of the program.

Implicitly typed variables were added to C# to deal with some uncommon case circumstances, the most significant of which relate to LINQ (language-integrated query), which is described later in this book. For most variables, you should use explicitly typed variables because they make your code simpler to read and more clear. Implicitly typed variables ought to be used just when fundamental. They are not intended to replace ordinary variable declarations in general. Generally, use, however don't abuse, this new C# feature. One final point: Only one implicitly typed variable can be declared at any one time.

## Variable Scope

Up until this point, the entirety of the variables that we have been using are declared toward the beginning of the Main( ) method. Be that as it may, C# enables a local variable to be declared inside any block. As clarified in Section 1, a block is started with an opening curly brace and finished with an ending curly brace.

A block defines a scope. In this way, each time you start another block, you are making another scope. A scope determines what names are visible to different parts of your program. It additionally determines the lifetime of local variables. The most significant scopes in C# are those characterized by a class and those characterized by a method. A dialog of class scope (and variables declared inside it) is deferred until later in this book, when classes are portrayed. For the time being, we will analyze just the scopes characterized by or inside a method.

The scope characterized by a method starts with its opening curly brace and finishes with its closing curly brace. Be that as it may, if that method has parameters, they, as well, are incorporated inside the scope characterized by the method. When in doubt, local variables declared inside a scope are not visible to code that is characterized outside that scope. Accordingly, when you declare a variable inside a scope, you are preventing it from being accessed or altered by code outside the scope. For sure, the scope rules give the foundation for encapsulation.

Scopes can be nested. For instance, each time you make a block of code, you are making another, nested scope. At the point when this happens, the outer scope encloses the inner scope. This implies that local variables declared in the outer scope will be visible to code inside the inner scope. In any case, the reverse isn't valid. Local variables declared inside the inner scope won't be visible outside it.

As the remarks demonstrate, the variable x is declared toward the beginning of Main( )'s scope and is open to all subsequent code inside Main( ). Inside the if block, y is declared. Since a block characterizes a scope, y is visible just to other code inside its block. This is the reason outside of its block, the line y = 100; is commented out. In the event that you remove the main comment symbol, a compile-time error will happen because y isn't visible outside of its block. Inside the if block, x can be used because code inside a block (that is, a nested scope) approaches variables declared by an enclosing scope.

In the event that you come from a C/C++ foundation, you realize that there is no restriction on the names that you give variables declared in an inner scope. Accordingly, in C/C++, the declaration of count inside the block of the outer for loop is totally legitimate. Be that as it may, in C/C++, such a declaration shadows the outer count. The architects of C# felt that this kind of name shadowing
