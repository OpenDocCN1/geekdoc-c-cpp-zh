
### Extending `sizeof`

The `sizeof` operator returns the number of bytes used to store an object. C++0x allows `sizeof` to be called on a data member without accessing it through an instance of the class it’s a part of. `sizeof` can also be used more naturally with `static` data members.

### Alternative to Sequence Points

The C++ standard describes the order in which operations occur in a program using the term “sequence points.” Many C++ experts think the wording fails to clearly describe the required sequence of events in the execution of a program. This proposal changes the wording in the standard to define the sequencing requirements more precisely. This issue is important to C++ because any future attempt to add concurrency (i.e., multithreading) requires a solid understanding of the order of events in a program.

### 21.12 Wrap-Up

In this chapter we discussed various aspects of the future of C++. We introduced the Boost C++ Libraries and described the Boost libraries that are included in TR1—the additions to the C++ Standard Library.

We discussed the `Boost.Regex` library and the symbols that are used to form regular expressions. We provided examples of how to use `Boost.Regex` classes, including `regex`, `match_results` and `regex_token_iterator`. You learned how to find patterns in a string and match entire strings to patterns with `Boost.Regex` algorithms `regex_search` and `regex_match`. We demonstrated how to replace characters in a string with `regex_replace` and how to split strings into tokens with a `regex_token_iterator`.

We gave examples of how to use the `Boost.Smart_ptr` library. We discussed the smart pointers included in TR1, namely `shared_ptr` and `weak_ptr`. We showed you how to use these classes to avoid memory leaks when using dynamically allocated memory. We demonstrated how to use custom deleter functions to allow `shared_ptr`s to manage resources that require special destruction procedures. We also explained how `weak_ptr`s can be used to prevent memory leaks in circularly referential data.

We overviewed the upcoming revised standard, C++0x, discussing TR1 and the changes to the core language. We introduced each of the libraries accepted into TR1. We described the new core language features including the `auto` keyword, *rvalue* reference, improvements in compatibility with C99, additional integer types and the new concept of conditionally supported behavior. Remember that Boost, TR1 and C++0x are constantly changing—visit our Resource Centers to stay up to date with all three.

In the next chapter, we discuss several more advanced C++ features, including cast operators, namespaces, operator keywords, pointer-to-class-member operators, multiple inheritance and virtual base classes.

- 33. Jens Maurer, “Extending sizeof to Apply to Non-Static Data Members Without an Object,” Document Number N2150=07-0010, January 7, 2007, www.open-std.org/jtc1/sc22/wg21/docs/papers/2007/n2150.html.
- 34. Clark Nelson, “A Finer-Grained Alternative to Sequence Points,” Document Number N1944=06-0014, February 17, 2006, www.open-std.org/jtc1/sc22/wg21/docs/papers/2006/n1944.htm.

## Other Topics

> *What’s in a name? that*  
> *which we call a rose*  
> *By any other name would*  
> *smell as sweet.*  
>  
> —William Shakespeare  
>  
> *O Diamond! Diamond!*  
> *thou little knowest the*  
> *mischief done!*  
>  
> —Sir Isaac Newton

### OBJECTIVES

In this chapter you’ll learn:

- To use `const_cast` to temporarily treat a `const` object as a non-const object.
- To use namespaces.
- To use operator keywords.
- To use mutable members in const objects.
- To use class-member pointer operators `.*` and `->*`.
- To use multiple inheritance.
- The role of virtual base classes in multiple inheritance.

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_911_0.png)

- 22.1 Introduction
- 22.2 const_cast Operator
- 22.3 namespaces
- 22.4 Operator Keywords
- 22.5 mutable Class Members
- 22.6 Pointers to Class Members ( .* and ->* )
- 22.7 Multiple Inheritance
- 22.8 Multiple Inheritance and virtual Base Classes
- 22.9 Wrap-Up

### 22.1 Introduction

We now consider several advanced C++ features. First, you’ll learn about the const_cast operator, which allows programmers to add or remove the const qualification of a variable. Next, we discuss namespaces, which can be used to ensure that every identifier in a program has a unique name and can help resolve naming conflicts caused by using libraries that have the same variable, function or class names. We then present several operator keywords that are useful for programmers who have keyboards that do not support certain characters used in operator symbols, such as !, &, ^, ~ and |. We continue our discussion with the mutable storage-class specifier, which enables a programmer to indicate that a data member should always be modifiable, even when it appears in an object that is currently being treated as a const object by the program. Next we introduce two special operators that we can use with pointers to class members to access a data member or member function without knowing its name in advance. Finally, we introduce multiple inheritance, which enables a derived class to inherit the members of several base classes. As part of this introduction, we discuss potential problems with multiple inheritance and how virtual inheritance can be used to solve those problems.

### 22.2 const_cast Operator

C++ provides the const_cast operator for casting away const or volatile qualification. You declare a variable with the volatile qualifier when you expect the variable to be modified by hardware or other programs not known to the compiler. Declaring a variable volatile indicates that the compiler should not optimize the use of that variable because doing so could affect the ability of those other programs to access and modify the volatile variable.

In general, it is dangerous to use the const_cast operator, because it allows a program to modify a variable that was declared const, and thus was not supposed to be modifiable. There are cases in which it is desirable, or even necessary, to cast away const-ness. For example, older C and C++ libraries might provide functions that have non-const parameters and that do not modify their parameters. If you wish to pass const data to such a function, you would need to cast away the data’s const-ness; otherwise, the compiler would report error messages.

Similarly, you could pass non-const data to a function that treats the data as if it were constant, then returns that data as a constant. In such cases, you might need to cast away the const-ness of the returned data, as we demonstrate in Fig. 22.1.

In this program, function maximum (lines 11–14) receives two C-style strings as const char * parameters and returns a const char * that points to the larger of the two strings. Function main declares the two C-style strings as non-const char arrays (lines 18–19); thus, these arrays are modifiable. In main, we wish to output the larger of the two C-style strings, then modify that C-style string by converting it to uppercase letters.

Function maximum’s two parameters are of type const char *, so the function’s return type also must be declared as const char *. If the return type is specified as only char *, the compiler issues an error message indicating that the value being returned cannot be converted from const char * to char *—a dangerous conversion, because it attempts to treat data that the function believes to be const as if it were non-const data.

```
// Fig. 22.1: fig22_01.cpp
// Demonstrating const_cast.
#include <iostream>
using std::cout;
using std::endl;

#include <cstring> // contains prototypes for functions strcmp and strlen
#include <cctype> // contains prototype for function toupper

// returns the larger of two C-style strings
const char *maximum( const char *first, const char *second )
{
    return ( strcmp( first, second ) >= 0 ? first : second );
} // end function maximum

int main()
{
    char s1[] = "hello"; // modifiable array of characters
    char s2[] = "goodbye"; // modifiable array of characters

    // const_cast required to allow the const char * returned by maximum
    // to be assigned to the char * variable maxPtr
    char *maxPtr = const_cast< char * >( maximum( s1, s2 ) );

    cout << "The larger string is: " << maxPtr << endl;

    for ( size_t i = 0; i < strlen( maxPtr ); i++ )
        maxPtr[ i ] = toupper( maxPtr[ i ] );

    cout << "The larger string capitalized is: " << maxPtr << endl;
    return 0;
} // end main
```

The larger string is: hello  
The larger string capitalized is: HELLO
