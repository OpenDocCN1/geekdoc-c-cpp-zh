
the system tries to summarize as many steps as possible and complete them all at once. With std::endl, you ensure that the system really outputs everything that has occurred.

### 4.2.15 The “std” Namespace

Now there is one more thing I need to explain to you before we dive deeper into the individual topics. In Listing 4.2, you can see using namespace std. With this tool, you save yourself the std:: in front of identifiers that you would otherwise have needed.

```cpp
#include <iostream>                 // for std::cin, std::cout, std::endl
#include <string>                   // for std::stoi
void calculate(int n) {
    using namespace std;            // for std::cout and std::endl
    /* output divisors */
    cout << "divisors of " << n << " are:\n";  // cout instead of std::cout
    for(int divisor=1; divisor <= n; ++divisor) {
        if(n % divisor == 0)
            cout << divisor << ", ";    // cout instead of std::cout
    }
    cout << endl;
}
```

Listing 4.21 You can include a namespace to make program text shorter.

Normally, the compiler checks for each identifier whether its name exists locally or on the outer levels. For example, divisor is a local variable and n is a parameter within the function. If you were to use cout without using, the compiler would check whether there is a local variable or a parameter with this name, then whether a global variable cout exists, and then inform you with an error that this is not the case—and that the identifier is therefore unknown.

With using, for each identifier that could not be found, the system tries whether it works with a preceding std::. This can save you a lot of typing, where you would otherwise type a lot of std::s.

The using namespace directive has an effect within the range in which it is defined—in the example, only within the calculate function. You can also write using namespace globally, in which case the scope is larger.

```cpp
#include <iostream>
#include <string>
using namespace std;            // has a global effect; works, but is critical
void calculate(int n) {
    /* output divisors */
    cout << "divisors of " << n << " are:\n";
    //...
}
// ... also in other functions ...
```

Listing 4.22 You can also use “using namespace” globally, but you should rarely do so.

Does that sound so tempting that you want to use using namespace ... all the time? Don’t do that! With using namespace ... you no longer know where the identifiers of your program come from. For example, if you are not yet familiar with the standard library and come across a free-standing cout, how are you supposed to know that it is actually std::cout?

> **Avoid Global “using namespace”**
>
> Do not use using namespace ... at a global level in a file. When reading each identifier, you ask yourself where it comes from, and you have no chance of finding out even by searching in the current file.
>
> Within a block—for example, locally in a function, as I have shown in Listing 4.21—a using namespace ... is not frowned upon, however. The range for wondering which namespace an identifier comes from is limited enough. And the probability that several using namespaces are active at the same time is lower.

But there is a solution: do not get all the identifiers of a namespace, but only the identifiers that you need, as in the following example.

```cpp
#include <iostream>              // cin, cout, endl
using std::endl;                 // applies globally in this file
void calculate(int n) {
    using std::cout;             // applies locally in this function
    /* output divisor */
    cout << "divisors of " << n << " are:\n";
    for(int divisor=1; divisor <= n; ++divisor) {
        if(n % divisor == 0)
            cout << divisor << ", ";
    }
    cout << endl;
}
```

Listing 4.23 Get individual identifiers with “using.”

Including identifiers in this way causes few problems. If a standalone cout appears somewhere in the file, you can find the original namespace with a simple search within the file.

## In This Book

As the listings in this book rarely become long and confusing, I will make an exception here. It saves space and repetition to write `using ...` at the beginning after the includes. Therefore, I will mainly abbreviate `std::cout`, `std::endl`, and `std::string` but will write out other identifiers with `std::` so that you know where they come from.

## 4.3 Operators

One- and two-character operators are very often used in expressions. 3+4 is a simple example, but an expression such as `!isBad && (x >= 0) && (x <= 1)` could also appear. You can achieve a lot in C++ with such sequences of operators and operands. Now that you know a lot about variables, types, and expressions, you should get to know the possible operators.

As an example, I will explain operators mainly using the int and bool types so that you get to know the repertoire first. However, many operators can also be applied to other types. These include built-in types, such as float, but also types from the standard library, such as `std::string` and `std::ostream`.

In C++, you can define your own types that also support operators. It is up to you to ensure that these then also do something that applies to the built-in types. For example, we expect + to perform an addition—like with an int. However, the class string uses + for concatenation, which is still “addition-like.” But you can, if you want, write a class Image that stores itself in a file with + followed by a string. (Please don’t do this!) We will deal with this in a suitable place. Here you will first find out what operators there are.

### Operators for Built-In Types Cannot Be Overwritten

When I describe operators in this chapter, I therefore mean those for the built-in types. You cannot change these in C++. There is already a + for int, and you as a programmer cannot change its meaning. In some places, I refer to the types of the standard library, but for many things, the reference must serve.

### 4.3.1 Operators and Operands

An operator is something that behaves like a function, but without being one. What is different is that you would expect a function to have its name at the front and the arguments in brackets after it, i.e. `func(arg1, arg2)`. With a little creative freedom, you could write `func` in the middle and omit the brackets, and you would get `arg1 func arg2`. And if the function name were + instead of func, you would have an operator + with its two operands arg1 and arg2.

Most operators are written with symbols, such as + or <<. Many have two arguments and are therefore called *binary operators*. In C++ it always looks like this:

- *Operand operator symbol operand*

If they are *unary operators*, the operator is placed before the operand as in -4 or, more rarely, after it as in idx++;

- *Operator symbol operand*
- *Operand operator symbol*

There are other forms of operators, which are explained next.

### 4.3.2 Overview of Operators

The operator symbols can be divided into several groups:

- **Arithmetic operators**  
  These are the four basic arithmetic operators +, -, *, and /, plus % for the remainder of the division (modulo). You can influence the sign with the unary operators + and -.
- **Bitwise arithmetic**  
  You can combine numbers bit by bit with |, &, ^, ~, <<, and >>.
- **Compound assignment**  
  In addition to =, there are also assignments that perform another operation at the same time. These are *compound assignments*: +=, -=, *=, /=, %=, >>=, <<=, &=, ^=, and |=.
- **Increment and decrement**  
  The two single-character operators ++ and -- are each available in a prefixed and a postfixed variant (prefix and postfix). If possible, prefer the prefix variant, as it does not require a temporary variable.
- **Relational operators**  
  Relational operators perform a comparison and return a truth value bool: ==, <, >, <=, >=, or !=. If you are working with the standard library, == and < are the most important, as many algorithms only use these two to derive the others if necessary. This is important if you want to make your own data types fit with the standard library.
- **Logical operators**  
  &&, ||, and ! combine truth values to form more complex expressions.
- **Pointer operator and dereference operator**  
  You use the unary operators & and * and the binary operators -> and . to address and to dereference. This means that you retrieve an address, turn an address into data, or access a structure. You will see their use in detail later.
