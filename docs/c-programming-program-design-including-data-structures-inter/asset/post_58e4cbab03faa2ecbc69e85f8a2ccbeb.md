
## Program Style and Form

In previous sections, you learned enough C++ concepts to write meaningful programs. Before beginning to write programs, however, you need to learn their proper structure, among other things. Using the proper structure for a C++ program makes it easier to understand and subsequently modify the program. There is nothing more frustrating than trying to follow and perhaps modify a program that is syntactically correct but has no structure.

In addition, every C++ program must satisfy certain rules of the language. A C++ program must contain the function main. It must also follow the syntax rules, which, like grammar rules, tell what is right and what is wrong and what is legal and what is illegal in the language. Other rules serve the purpose of giving precise meaning to the language; that is, they support the language's semantics.

The following sections are designed to help you learn how to use the C++ programming elements you have learned so far to create a functioning program. These sections cover the syntax; the use of blanks; the use of semicolons, brackets, and commas; semantics; naming identifiers; prompt lines; documentation, including comments; and form and style.

### Syntax

The syntax rules of a language tell what is legal and what is not legal. Errors in syntax are detected during compilation. For example, consider the following C++ statements:

```cpp
int x;          //Line 1
int y;          //Line 2
double z;       //Line 3

y = w + x;      //Line 4
```

When these statements are compiled, a compilation error will occur at Line 2 because the semicolon is missing after the declaration of the variable y. A second compilation error will occur at Line 4 because the identifier w is used but has not been declared.

As discussed in Chapter 1, you enter a program into the computer by using a text editor. When the program is typed, errors are almost unavoidable. Therefore, when the program is compiled, you are most likely to see syntax errors. It is quite possible that a syntax error at a particular place might lead to syntax errors in several subsequent statements. It is very common for the omission of a single character to cause four or five error messages. However, when the first syntax error is removed and the program is recompiled, subsequent syntax errors caused by this syntax error may disappear. Therefore, you should correct syntax errors in the order in which the compiler lists them. As you become more familiar and experienced with C++, you will learn how to quickly spot and fix syntax errors. Also, compilers not only discover syntax errors, but also hint and sometimes tell the user where the syntax errors are and how to fix them.

### Use of Blanks

In C++, you use one or more blanks to separate numbers when data is input. Blanks are also used to separate reserved words and identifiers from each other and from other symbols. Blanks must never appear within a reserved word or identifier.

### Use of Semicolons, Brackets, and Commas

All C++ statements must end with a semicolon. The semicolon is also called a **statement terminator**.

Note that curly braces, `{` and `}`, are not C++ statements in and of themselves, even though they often appear on a line with no other code. You might regard brackets as delimiters, because they enclose the body of a function and set it off from other parts of the program. Brackets have other uses, which will be explained in Chapter 4.

Recall that commas are used to separate items in a list. For example, you use commas when you declare more than one variable following a data type.

### Semantics

The set of rules that gives meaning to a language is called **semantics**. For example, the order-of-precedence rules for arithmetic operators are semantic rules.

If a program contains syntax errors, the compiler will warn you. What happens when a program contains semantic errors? It is possible to eradicate all syntax errors in a program and still have it run. And if it runs, it may not do what you meant it to do. For example, the following two lines of code are both syntactically correct expressions, but they have different meanings:

```cpp
2 + 3 * 5
```

and:

```cpp
(2 + 3) * 5
```

If you substitute one of these lines of code for the other in a program, you will not get the same results—even though the numbers are the same, the semantics are different. You will learn about semantics throughout this book.

### Naming Identifiers

Consider the following two sets of statements:

```cpp
const double A = 2.54;      //conversion constant
double x;                 //variable to hold centimeters
double y;                 //variable to hold inches

x = y * a;
```

only tells the user to input a number, but also informs the user that the number should be between 1 and 10.

### Documentation

The programs that you write should be clear not only to you, but also to anyone else. Therefore, you must properly document your programs. A well-documented program is easier to understand and modify, even a long time after you originally wrote it. You use comments to document programs. Comments should appear in a program to explain the purpose of the program, identify who wrote it, and explain the purpose of particular statements.

### Form and Style

You might be thinking that C++ has too many rules. However, in practice, the rules give C++ a great degree of freedom. For example, consider the following two ways of declaring variables:

```cpp
int feet, inches;
double x, y;
```

and

```cpp
int feet,inches;double x,y;
```

The computer would have no difficulty understanding either of these formats, but the first form is easier to read and follow. Of course, the omission of a single comma or semicolon in either format may lead to all sorts of strange error messages.

What about blank spaces? Where are they significant and where are they meaningless? Consider the following two statements:

```cpp
int a,b,c;
```

and

```cpp
int    a,   b,   c;
```

Both of these declarations mean the same thing. Here, the blanks between the identifiers in the second statement are meaningless. On the other hand, consider the following statement:

```cpp
inta,b,c;
```

This statement contains a syntax error. The lack of a blank between int and the identifier a changes the reserved word int and the identifier a into a new identifier, inta.

The clarity of the rules of syntax and semantics frees you to adopt formats that are pleasing to you and easier to understand.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_135_0.png)

The following example further elaborates on this.

### EXAMPLE 2-30

Consider the following C++ program:

```cpp
//An improperly formatted C++ program.

#include <iostream>
#include <string>
using namespace std;

int main()
{
int num; double height;
string name;
cout << "Enter an integer: "; cin >> num; cout << endl;
    cout<<"num: "<<num<<endl;
cout<<"Enter the name: "; cin>>name;
    cout<<endl; cout <<"Enter the height: ";
cin>>height; cout <<endl;

cout<<"Name: "<<name<<endl; cout<<"Height: "
<<height; cout <<endl;return 0;
}
```

This program is syntactically correct. The C++ compiler would have no difficulty reading and compiling this program. However, this program is very hard to read. The program that you write should be properly indented and formatted. Note the difference when the program is formatted:

```cpp
//A properly formatted C++ program.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    int num;
    double height;
    string name;

    cout << "Enter an integer: ";
    cin >> num;
    cout << endl;
    cout << "num: " << num << endl;

    cout << "Enter the first name: ";
    cin >> name;
    cout << endl;
    cout << "Enter the height: ";
    cin >> height;
    cout << endl;

    cout << "Name: " << name << endl;
    cout << "Height: " << height << endl;

    return 0;
}
```

As you can see, this program is easier to read. Your programs should be properly indented and formatted. To document the variables, programmers typically declare one variable per line. Also, always put a space before and after an operator. When you type your program using an IDE, typically, your program is automatically indented.

### More on Assignment Statements

The assignment statements you have seen so far are called **simple assignment statements**. In certain cases, you can use special assignment statements called **compound assignment statements** to write simple assignment statements in a more concise notation.

Corresponding to the five arithmetic operators +, -, *, /, and %, C++ provides five compound operators: +=, -=, *=, /=, and %=, respectively. Consider the following simple assignment statement, in which x and y are int variables:

```cpp
x = x * y;
```

Using the compound operator *=, this statement can be written as:

```cpp
x *= y;
```

In general, using the compound operator *=, you can rewrite the simple assignment statement:

```cpp
variable = variable * (expression);
```

as:

```cpp
variable *= expression;
```
