
An increment or decrement operator placed before (prefixed to) a variable is called the prefix increment or prefix decrement operator, respectively. An increment or decrement operator placed after (postfixed to) a variable is called the postfix increment or postfix decrement operator, respectively.

Using the prefix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable preincrements (or predecrements) the variable. The variable is incremented (or decremented) by 1, then its new value is used in the expression in which it appears.

Using the postfix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable postincrements (or postdecrements) the variable. The variable’s value before the increment (or decrement) is used in the expression. Unlike binary operators, the unary increment and decrement operators by convention should be placed next to their operands, with no intervening spaces.

### Prefix Increment vs. Postfix Increment

Figure 3.4 demonstrates the difference between the prefix increment and postfix increment versions of the ++ increment operator. The decrement operator (--) works similarly.

```cpp
// fig03_04.cpp
// Prefix increment and postfix increment operators.
#include <iostream>
using namespace std;

int main() {
    // demonstrate postfix increment operator
    int c{5};
    cout << "c before postincrement: " << c << "\n"; // prints 5
    cout << "    postincrementing c: " << c++ << "\n"; // prints 5
    cout << "c after postincrement: " << c << "\n"; // prints 6

    cout << "\n"; // skip a line

    // demonstrate prefix increment operator
    c = 5;
    cout << "c before preincrement: " << c << "\n"; // prints 5
    cout << "    preincrementing c: " << ++c << "\n"; // prints 6
    cout << "c after preincrement: " << c << "\n"; // prints 6
}
```

```text
c before postincrement: 5
    postincrementing c: 5
c after postincrement: 6

c before preincrement: 5
    preincrementing c: 6
c after preincrement: 6
```

**Fig. 3.4** | Prefix increment and postfix increment operators.

Line 8 initializes the variable c to 5, and line 9 outputs c’s initial value. Line 10 outputs the value of the expression c++. This expression postincrements the variable c, so c’s original value (5) is output, then c’s value is incremented (to 6). Thus, line 10 outputs c’s initial value (5) again. Line 11 outputs c’s new value (6) to prove that the variable’s value was incremented in line 10. Line 16 resets c’s value to 5, and line 17 outputs c’s value. Line 18 outputs the value of the expression ++c. This expression preincrements c, so its value is incremented. Then the new value (6) is output. Line 19 outputs c’s value again to show that c is still 6 after line 18 executes.

### Simplifying Statements with the Arithmetic Compound Assignment, Increment and Decrement Operators

The arithmetic compound assignment operators and the increment and decrement operators can be used to simplify program statements. For example, the three assignment statements in Fig. 3.3 (lines 21, 24 and 28)

```cpp
passes = passes + 1;
failures = failures + 1;
studentCounter = studentCounter + 1;
```

can be written more concisely with compound assignment operators as

```cpp
passes += 1;
failures += 1;
studentCounter += 1;
```

with prefix increment operators as

```cpp
++passes;
++failures;
++studentCounter;
```

or with postfix increment operators as

```cpp
passes++;
failures++;
studentCounter++;
```

When incrementing or decrementing a variable in a statement by itself, the prefix increment and postfix increment forms have the same effect, and the prefix decrement and postfix decrement forms have the same effect. Only when a variable appears in the context of a larger expression does preincrementing or postincrementing the variable have a different effect (and similarly for predecrementing or postdecrementing).

Attempting to use the increment or decrement operator on an expression other than one to which a value can be assigned is a compilation error. For example, writing ++(x + 1) is a syntax error, because (x + 1) is not a variable.

### Operator Precedence and Grouping

The following table shows the precedence and grouping of the operators introduced to this point. The operators are shown top-to-bottom in decreasing order of precedence. The second column indicates the grouping of the operators at each level of precedence. Notice that the conditional operator (?:), the unary operators preincrement (++), predecrement (--), plus (+) and minus (-), and the assignment operators +=, -=, *=, /= and %= group right-to-left. All other operators in this table group left-to-right.

| Operators | Grouping |
|---|---|
| `++ (postfix)` `-- (postfix)` | left to right |
| `+` `-` `++ (prefix)` `-- (prefix)` | right to left |
| `*` `/` `%` | left to right |
| `+` `-` | left to right |
| `<<` `>>` | left to right |
| `<` `<=` `>` `>=` | left to right |
| `==` `!=` | left to right |
| `?:` | right to left |
| `=` `+=` `-=` `*=` `/=` `%=` | right to left |

### Checkpoint

- **1. (Code)** Assume the `int` variable `counter` has the value 10. What are the values of `result` and `counter` after this statement executes?

  ```cpp
  int result{counter--};
  ```

  **Answer:** The initialization expression uses the postdecrement operator, so `result` will contain 10 and `counter` will contain 9.

- **2. (Code)** Assume the `int` variable `counter` has the value 10. What are the values of `result` and `counter` after this statement executes?

  ```cpp
  int result{++counter};
  ```

  **Answer:** The initialization expression uses the preincrement operator, so both `result` and `counter` will contain 11.

## 3.13 Fundamental Types Are Not Portable

You can view the complete list of C++ fundamental types and their typical ranges at

https://en.cppreference.com/w/cpp/language/types

In C and C++, an `int` on one machine might be represented by 16 bits (2 bytes) of memory, on a second machine by 32 bits (4 bytes), and on another machine by 64 bits (8 bytes). For this reason, code using integers is not always portable across platforms. You could write multiple versions of your programs to use different integer types on different platforms. Or you could use techniques to achieve various levels of portability.⁶ In the next section, we’ll show one way to achieve portability.

Among C++’s integer types are `int`, `long` and `long long`. The C++ standard requires type `int` to be at least 16 bits, type `long` to be at least 32 bits and type `long long` to be at least 64 bits. The standard also requires that an `int`’s size be less than or equal to a `long`’s size and that a `long`’s size be less than or equal to a `long long`’s size. Such “squishy” requirements create portability challenges but allow compiler implementers to optimize performance by matching fundamental type sizes to your machine’s hardware.

### Checkpoint

- **1. *(True/False)*** All computers represent an `int` in the same number of bytes.

  **Answer:** False. An `int` on one machine might be represented by 16 bits (2 bytes) of memory, on a second machine by 32 bits (4 bytes), and on another machine by 64 bits (8 bytes).

- **2. *(True/False)*** The C++ standard requires that an `int`’s size be less than or equal to a `long`’s size and that a `long`’s size be less than or equal to a `long long`’s size.

  **Answer:** True.

## 3.14 Objects Natural Case Study: Super-Sized Integers

The explosive growth of Internet communications and data storage on Internet-connected devices has dramatically increased the importance of privacy and security. Cryptography has been used for thousands of years to encode data, making it difficult (and hopefully impossible) for unauthorized users to read,⁷,⁸ which is critically important in today’s connected world. Most websites (including deitel.com) now use HTTPS (HyperText Transfer Protocol Secure) to encrypt and decrypt your Internet interactions.

### Some Applications Need Integers Outside a long long Integer’s Range

Many cryptography algorithms perform calculations with integers far larger than we can store using even C++’s `long long` type. On most systems, a `long long` integer can store values in the range −9,223,372,036,854,775,808 to 9,223,372,036,854,775,807—a maximum of 19 decimal digits (which can represent integers in the quintillions).

One of the most popular encryption/decryption schemes is RSA Public-Key Cryptography, commonly used to secure data transmitted over the Internet.⁹,¹⁰,¹¹ Industrial-strength RSA implementations work with enormous prime numbers consisting of hundreds of digits.

A key reason why RSA is so secure is the sheer amount of time required to factor the product of those primes, even for today’s most powerful supercomputers. Public-key cryptography also is used to secure the blockchain technology behind cryptocurrencies like Bitcoin.¹² Later in the book, we’ll discuss and implement public-key cryptography with RSA.

- 7. “Cryptography.” January 15, 2023. https://en.wikipedia.org/wiki/Cryptography#History.

- 8. Binance Academy, “History of Cryptography.” Accessed April 14, 2023. https://www.binance.vision/security/history-of-cryptography.

- 9. “RSA (Cryptosystem).” Accessed April 14, 2023. https://en.wikipedia.org/wiki/RSA_(cryptosystem).

- 10. “RSA Algorithm.” Accessed April 14, 2023. https://simple.wikipedia.org/wiki/RSA_algorithm.

- 11. K. Moriarty, B. Kaliski, J. Jonsson and A. Rusch, “PKCS #1: RSA Cryptography Specifications Version 2.2,” November 2016. Accessed April 14, 2023. https://tools.ietf.org/html/rfc8017.

- 12. Sarah Rothrie, “How Blockchain Cryptography Is Fighting the Rise of Quantum Machines,” December 28, 2018. Accessed April 14, 2023. https://coincentral.com/blockchain-cryptography-quantum-machines/.
