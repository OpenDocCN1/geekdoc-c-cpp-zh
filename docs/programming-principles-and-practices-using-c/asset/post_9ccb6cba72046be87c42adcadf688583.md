
# Postscript

As it happens, we have now seen a simple example of how a compiler works. The calculator analyzes input broken down into tokens and understood according to a grammar. That's exactly what a compiler does. After analyzing its input, a compiler then produces a representation (object code) that we can later execute. The calculator immediately executes the expressions it has analyzed; programs that do this are called interpreters rather than compilers.

# 8 Technicalities: Functions, etc.

> “No amount of genius can overcome obsession with detail.”
> — *Traditional*

In this chapter and the next, we change our focus from programming to our main tool for programming: the C++ programming language. We present language-technical details to give a slightly broader view of C++'s basic facilities and to provide a more systematic view of those facilities. These chapters also act as a review of many of the programming notions presented so far and provide an opportunity to explore our tool without adding new programming techniques or concepts.

## 8.1 Technicalities

Given a choice, we’d much rather talk about programming than about programming language features; that is, we consider how to express ideas as code far more interesting than the technical details of the programming language that we use to express those ideas. To pick an analogy from natural languages: we’d much rather discuss the ideas in a good novel and the way those ideas are expressed than study the grammar and vocabulary of English. What matters are ideas and how those ideas can be expressed in code, not the individual language features.

However, we don’t always have a choice. When you start programming, your programming language is a foreign language for which you need to look at “grammar and vocabulary.” This is what we will do in this chapter and the next, but please don’t forget:

- Our primary study is programming.
- Our output is programs/systems.
- A programming language is (only) a tool.

Keeping this in mind appears to be amazingly difficult. Many programmers come to care passionately about apparently minor details of language syntax and semantics. In particular, too many get the mistaken belief that the way things are done in their first programming language is “the one true way.” Please don’t fall into that trap. C++ is in many ways a very nice language, but it is not perfect; neither is any other programming language.

Most design and programming concepts are universal, and many such concepts are widely supported by popular programming languages. That means that the fundamental ideas and techniques we learn in a good programming course carry over from language to language. They can be applied – with varying degrees of ease – in all languages. The language technicalities, however, are specific to a given language. Fortunately, programming languages do not develop in a vacuum, so much of what you learn here will have reasonably obvious counterparts in other languages. In particular, C++ belongs to a group of languages that also includes C (Chapter 27), Java, and C#, so quite a few techniques are shared with those languages.

Note that when we are discussing language-technical issues, we deliberately use nondescriptive names, such as $ \mathbf { f } $, $ \mathbf { g } $, $ \mathbf { x } $, and $ \mathbf { y } $. We do that to emphasize the technical nature of such examples, to keep those examples very short, and to try to avoid confusing you by mixing language technicalities and genuine program logic. When you see nondescriptive names (such as should never be used in real code), please focus on the language-technical aspects of the code. Technical examples typically contain code that simply illustrates language rules. If you compiled and ran them, you'd get many “variable not used” warnings, and few such technical program fragments would do anything sensible.

Please note that what we write here is not a complete description of C++'s syntax and semantics – not even for the facilities we describe. The ISO C++ standard is 1300+ pages of dense technical language and *The C++ Programming Language* by Stroustrup is 1300+ pages of text aimed at experienced programmers (both covering both the C++ language and its standard library). We do not try to compete with those in completeness and comprehensiveness; we compete with them in comprehensibility and value for time spent reading.

## 8.2 Declarations and definitions

A *declaration* is a statement that introduces a name into a scope (§8.4):

- Specifying a type for what is named (e.g., a variable or a function)
- Optionally, specifying an initializer (e.g., an initializer value or a function body)

For example:

```cpp
int a = 7;  // an int variable
const double cd = 8.7;  // a double-precision floating-point constant
double sqrt(double);  // a function taking a double argument
                      // and returning a double result
vector<Token> v;  // a vector-of-tokens variable
```

Before a name can be used in a C++ program, it must be declared. Consider:

```cpp
int main()
{
    cout << f(i) << '\n';
}
```

The compiler will give at least three “undeclared identifier” errors for this: `cout`, `f`, and `i` are not declared anywhere in this program fragment. We can get `cout` declared by including the header `std_lib_facilities.h`, which contains its declaration:

```cpp
#include "std_lib_facilities.h" // We find the declaration of cout in here
int main()
{
    cout << f(i) << '\n';
}
```

Now, we get only two “undefined” errors. As you write real-world programs, you'll find that most declarations are found in headers. That’s where we define interfaces to useful facilities defined “elsewhere.” Basically, a declaration defines how something can be used; it defines the interface of a function, variable, or class. Please note one obvious but invisible advantage of this use of declarations: we didn’t have to look at the details of how `cout` and its `<<` operators were defined; we just `#included` their declarations. We didn’t even have to look at their declarations; from textbooks, manuals, code examples, or other sources, we just know how `cout` is supposed to be used. The compiler reads the declarations in the header that it needs to “understand” our code.

However, we still have to declare `f` and `i`. We could do that like this:

```cpp
#include "std_lib_facilities.h" // We find the declaration of cout in here
int f(int);                 // declaration of f
int main()
{
    int i = 7;              // declaration of i
    cout << f(i) << '\n';
}
```

This will compile because every name has been declared, but it will not link (§2.4) because we have not defined `f()`; that is, nowhere have we specified what `f()` actually does.

A declaration that (also) fully specifies the entity declared is called a *definition*. For example:

```cpp
int a = 7;
vector<double> v;
double sqrt(double d) { /* ... */ }
```

Every definition is (by definition) also a declaration, but only some declarations are also definitions. Here are some examples of declarations that are not definitions; if the entity it refers to is used, each must be matched by a definition elsewhere in the code:

```cpp
double sqrt(double);    // no function body here
extern int a;
// “extern plus no initializer” means “not definition”
```

When we contrast definitions and declarations, we follow convention and use declarations to mean “declarations that are not definitions” even though that’s slightly sloppy terminology.

A definition specifies exactly what a name refers to. In particular, a definition of a variable sets aside memory for that variable. Consequently, you can’t define something twice. For example:

```cpp
double sqrt(double d) { /* ... */ }    // definition
double sqrt(double d) { /* ... */ }    // error: double definition
int a;                                 // definition
int a;                                 // error: double definition
```

In contrast, a declaration that isn’t also a definition simply tells how you can use a name; it is just an interface and doesn’t allocate memory or specify a function body. Consequently, you can declare something as often as you like as long as you do so consistently:

```cpp
int x = 7;                         // definition
extern int x;                      // declaration
extern int x;                      // another declaration

double sqrt(double);               // declaration
double sqrt(double d) { /* ... */ } // definition
double sqrt(double);               // another declaration of sqrt
double sqrt(double);               // yet another declaration of sqrt

int sqrt(double);                  // error: inconsistent declarations of sqrt
```

Why is that last declaration an error? Because there cannot be two functions called sqrt taking an argument of type double and returning different types (int and double).

The extern keyword used in the second declaration of x simply states that this declaration of x isn’t a definition. It is rarely useful. We recommend that you don’t
