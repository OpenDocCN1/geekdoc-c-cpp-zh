
This is already very “modern,” but you can also make it “purer.” In the next example, you can see the whole thing without the wrapper objects created by `make_shared`.

```cpp
// https://godbolt.org/z/E7e7qq1MY
Data* dataOwner = new Data(5);
Data* data = dataOwner;
Data* more = new Data(6);
data = more;
more->value = 7;
cout << data->value << '\n'; // now also 7
/* tidy up */
delete more;
delete dataOwner;
```

**Listing 3.4** C++: Without modern C++ tools, special attention must be paid to pointer ownership.

But oh dear: here you can already see what trouble you can get into if you have to handle cleanup yourself. `delete data` would have been wrong in the end, because data points to more, and that has already been cleared away. The assignment `data = more` is the villain that has hidden data. Release is no longer possible. This is the only reason that dataOwner exists, so that the original pointer can be released later.

Therefore, in C++, it is useful to adopt the concept of *ownership of pointers*: raw pointers always belong to someone who is responsible for clearing them away. Either this is the person who created the object with `new`, or the ownership is transferred. You can do this “in your head,” using tools such as the *Guideline Support Library* (GSL; see [Chapter 30](#) on guidelines), write wrapper classes yourself; or simply use the supplied tools such as `shared_ptr` and `unique_ptr`. In the next example, I choose `final`. In Java, this means that nothing new can be assigned to the reference.

```cpp
final Data data = new Data(5);
data.value = 7;             // that's okay
data = new Data(6);          // ✘ this prevents final
```

**Listing 3.5** In Java, final only blocks the reference.

In C++, const can be used in a much more differentiated way.

```cpp
// https://godbolt.org/z/Moe5M7sK8
Data const* data = new Data(5);
data->value = 7;            // this const protects Data
data = new Data(6);          // reassigning pointer is okay
Data * const more = new Data(8);
more->value = 9;        // now okay
more = new Data(10);   // reference is protected
```

**Listing 3.6** C++: const can protect the value or the reference.

In C++, both the reference or pointer and the content—that is, the value—can be protected. You can also combine both with `Data const * const`. You can recognize what is protected by the const **behind** it:

- `Data * const` more：The pointer or reference is protected.
- `Data const * data`：The value Data is protected.
- `const Data * data`：This is an alternative notation for `Data const * data`.
- `Data const * const more`：Both value and pointer are protected.

There are also variants of const: const methods may not change their own object, and constexpr forces the expression to be calculated by the compiler at compile time.

## Chapter 4
### The Basic Building Blocks of C++

- **Chapter Telegram**
  - **main**：The entry point to every program.
  - **#include**：Integration of other program parts and libraries.
  - **Variable**：Name for a memory area that can hold a value.
  - **Initialization**：This is the value that a variable will have when it is created. For built-in types, initialization is particularly important during definition as otherwise a variable will have an undefined state.
  - **Assignment**：A special *expression* that changes the content of a variable using `=`.
  - **return**：Exiting a function; in `main`, the end of the program.
  - **Comment**：A note to the program code that the compiler does not evaluate.
  - **Statement**：A program is the sequential processing of various statements.
  - **Expression**：A sequence of operations on operands for assignments and the like.
  - **Block**：A group of statements between curly braces.
  - **Type or data type**：For the compiler, every expression has a type.
  - **Standard library**：Part of the C++ standard and supplied with the compiler. Everything that is not pure syntax or semantics or a built-in data type is supplied by the standard library.
  - **Own function**：With a custom function, you outsource code to another location. This is the basis for clarity and reusability.
  - **Function parameter**：Gives the "thing" passed to a function its own local name within a function.
  - **Side effect operator**：Operator that changes the value of a variable but is not an assignment.
  - **int and bool**：Two elementary (built-in) and simple types.
  - **Unified initialization**：A unique notation for the first value of a variable or a default parameter.
  - **Token**：For the compiler, the smallest building blocks of the program text.
  - **Identifier**：Names of program elements—that is, variables, types, functions, and so on.
  - **for statement**：This is a way of implementing the repetition of statements.
  - **if statement**：You use this to implement branching.
  - **Operator**：Usually a symbol that stands between two operands (or in front of one); works like a function with the operands as arguments.
  - **Operand**：Argument for an operator.
  - **Arithmetic operator**：Used for classical arithmetic with +, -, *, /, and % as well as bitwise arithmetic with |, &, ^, <<, and >>.
  - **Relational operator**：Greater than, less than, equal to, combinations thereof and not equal to: >, <, ==, <=, >=, !=, or even <=> (C++20).
  - **Logical operator**：Combines Boolean values: &&, ||, and !.
  - **Assignment operator or compound assignment**：The assignment operator is the equal sign =. A compound assignment combines = with an arithmetic operator.
  - **Binary system**：The digit value number system of the computer using zeros and ones.
  - **Built-in type**：A type that is available to you without #include.
  - **Integer type**：One of short, int, long, or long long built-in types, each signed or unsigned.
  - **Floating-point type**：One of the float, double, or long double built-in types; since C++23, std::floatN_t.
  - **Character type**：Most often char, but also with `wchar_t`, `char16_t`, and `char32_t` international characters; all built-in types.
  - **Character string**：As literal `const char[]`, together with C often `const char*` in C++ strings; in each case, also possibly with one of the other character types.
  - **Truth value type**：The built-in type bool with its literals `true` and `false`.
  - **Type inference with auto**：When defining a variable, let the compiler determine the type from the type of the expression of the initialization.
  - **Overflow**：An attempt to change the value of a type beyond its value range; an overflow can occur in both the positive and negative range.
  - **Literal**：A value specified directly in the source text.
  - **using and typedef**：Defining a type abbreviation.

In this chapter, we will take a very quick “flight” over a simple C++ program. This will familiarize you with the most important elements and give you a better understanding of the things I will explain in the following chapters.

Let’s start with a simple C++ program.

```cpp
// https://godbolt.org/z/Mdj7bGvar
#include <iostream>                    // Include modules/libraries
int main()                              // main() is the start of the program
{
    int value = 100;                    // Variable with initial value
    std::cout << "Divisors of " << value << " are:\n"; // Output of text
    for(int divider=1; divider <= value; divider = divider+1) // loop from 1 to 100
    {
        if(value % divider == 0)        // test for conditional execution
            std::cout << divider << ", "; // only if the test is positive
    }                                   // end of the loop
    std::cout << "\n";                  // single output
    return 0;                           // means end of program in main()
}                                       // end of main()
```

**Listing 4.1** A very simple C++ program.
