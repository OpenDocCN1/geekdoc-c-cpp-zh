
To handle cases where the value of a “variable” that is initialized with a value that is not known at compile time but never changes after initialization, C++ offers a second form of constant (a **const**):

```cpp
constexpr int max = 100;

void use(int n)
{
      constexpr int c1 = max+7;   // OK: c1 is 107
      const int c2 = n+7;   // OK, but don't try to change the value of c2
      // ...
      c2 = 7;                     // error: c2 is a const
}
```

Such “**const** variables” are very common for two reasons:

- C++98 did not have **constexpr**, so people used **const**.
- “Variables” that are not constant expressions (their value is not known at compile time) but do not change values after initialization are in themselves widely useful.

## 4.3.2 Operators

We just used the simplest operators. However, you will soon need more as you want to express more complex operations. Most operators are conventional, so we’ll just explain them later as needed and you can look up details if and when you find a need. Here is a list of the most common operators:

| Name | Comment |
|---|---|
| **f**(a) | function call: pass a to f as an argument |
| **++lval** | pre-increment: increment and use the incremented value |
| **--lval** | pre-decrement: decrement and use the decremented value |
| **!a** | not: result is bool |
| **-a** | unary minus |
| **a\*b** | multiply |
| **a/b** | divide |
| **a%b** | modulo (remainder): only for integer types |
| **a+b** | add |
| **a-b** | subtract |
| **out<<b** | write b to out: where out is an ostream |
| **in>>b** | read from in into b: where in is an istream |
| **a<b** | less than: result is bool |
| **a<=b** | less than or equal: result is bool |
| **a>b** | greater than: result is bool |
| **a>=b** | greater than or equal: result is bool |
| **a==b** | equal: not to be confused with = |
| **a!=b** | not equal: result is bool |
| **a && b** | logical and: result is bool |
| **a \|\| b** | logical or: result is bool |
| **lval = a** | assignment: not to be confused with == |
| **lval \*= a** | compound assignment: lval = lval\*a; also for /, %, +, - |

We used lval (short for “value that can appear on the left-hand side of an assignment”) where the operator modifies an operand. You can find a complete list in §A.5.

For examples of the use of the logical operators && (and), || (or), and ! (not), see §5.5.1, §7.7, §7.8.2, and §10.4.

Note that a<b<c means (a<b)<c and that a<b evaluates to a Boolean value: true or false. So, a<b<c will be equivalent to either true<c or false<c. In particular, a<b<c does not mean “Is b between a and c?” as many have naively (and not unreasonably) assumed. Thus, a<b<c is basically a useless expression. Don’t write such expressions with two comparison operations, and be very suspicious if you find such an expression in someone else’s code – it is most likely an error.

An increment can be expressed in at least three ways:

```cpp
++a
a+=1
a=a+1
```

Which notation should we use? Why? We prefer the first version, ++a, because it more directly expresses the idea of incrementing. It says what we want to do (increment a) rather than how to do it (add 1 to a and then write the result to a). In general, a way of saying something in a program is better than another if it more directly expresses an idea. The result is more concise and easier for a reader to understand. If we wrote a=a+1, a reader could easily wonder whether we really meant to increment by **1**. Maybe we just mistyped **a=b+1**, **a=a+2**, or even **a=a-1**; with **++a** there are far fewer opportunities for such doubts. Please note that this is a logical argument about readability and correctness, not an argument about efficiency. Contrary to popular belief, modern compilers tend to generate exactly the same code from **a=a+1** as for **++a** when **a** is one of the built-in types. Similarly, we prefer **a\*=scale** over **a=a\*scale**.

## 4.3.3 Conversions

We can “mix” different types in expressions. For example, **2.5/2** is a **double** divided by an **int**. What does this mean? Do we do integer division or floating-point division? Integer division throws away the remainder; for example, **5/2** is **2**. Floating-point division is different in that there is no remainder to throw away; for example, **5.0/2.0** is **2.5**. It follows that the most obvious answer to the question “Is **2.5/2** integer division or floating-point division?” is “Floating-point, of course; otherwise we’d lose information.” We would prefer the answer **1.25** rather than **1**, and **1.25** is what we get. The rule (for the types we have presented so far) is that if an operator has an operand of type **double**, we use floating-point arithmetic yielding a **double** result; otherwise, we use integer arithmetic yielding an **int** result. For example:

```text
5/2 is 2  (not 2.5)

2.5/2 means 2.5/double(2), that is, 1.25

'a'+1 means int('a')+1
```

The notations **type(value)** and **type{value}** mean “convert **value** to **type** as if you were initializing a variable of type **type** with the value **value**.” In other words, if necessary, the compiler converts (“promotes”) **int** operands to **doubles** or **char** operands to **ints**. The **type(value)** notation prevents narrowing (§3.9.2), but the **type{value}** notation does not. Once the result has been calculated, the compiler may have to convert it (again) to use it as an initializer or the right hand of an assignment. For example:

```cpp
double d = 2.5;
int i = 2;

double d2 = d/i;    // d2 == 1.25
int i2 = d/i;        // i2 == 1
int i3 {d/i};        // error: double -> int conversion may narrow (§3.9.2)

d2 = d/i;            // d2 == 1.25
i2 = d/i;            // i2 == 1
```

Beware that it is easy to forget about integer division in an expression that also contains floating-point operands. Consider the usual formula for converting degrees Celsius to degrees Fahrenheit: $f = 9/5 * c + 32$. We might write

```cpp
double dc;
cin >> dc;
double df = 9/5*dc+32;   // beware!
```

Unfortunately, but quite logically, this does not represent an accurate temperature scale conversion: the value of 9/5 is 1 rather than the 1.8 we might have hoped for. To get the code mathematically correct, either 9 or 5 (or both) will have to be changed into a double. For example:

```cpp
double dc;
cin >> dc;
double df = 9.0/5*dc+32;   // better
```

## 4.4 Statements

An expression computes a value from a set of operands using operators like the ones mentioned in §4.3. What do we do when we want to produce several values? When we want to do something many times? When we want to choose among alternatives? When we want to get input or produce output? In C++, as in many languages, you use language constructs called statements to express those things.

So far, we have seen two kinds of statements: expression statements and declarations. An expression statement is simply an expression followed by a semicolon. For example:

```cpp
a = b;
++b;
```

Those are two expression statements. Note that the assignment = is an operator so that a=b is an expression and we need the terminating semicolon to make a=b; a statement. Why do we need those semicolons? The reason is largely technical. Consider:

```cpp
a = b + + b;    // syntax error: missing semicolon
```

Without the semicolon, the compiler doesn't know whether we mean a=b++; b; or a=b; ++b;. This kind of problem is not restricted to computer languages; consider the exclamation “man eating tiger!” Who is eating whom? Punctuation exists to eliminate such problems, for example, “man-eating tiger!”

When statements follow each other, the computer executes them in the order in which they are written. For example:

```cpp
int a = 7;
cout << a << "\n";
```

Here the declaration, with its initialization, is executed before the output expression statement.

In general, we want a statement to have some effect. Statements without effect are typically useless. For example:

```cpp
1+2;        // do an addition, but don't use the sum
a*b;        // do a multiplication, but don't use the product
```

Such statements without effects are typically logical errors, and compilers often warn against them. Thus, expression statements are typically assignments, I/O statements, or function calls.

We will mention one more type of statement: the "empty statement." Consider the code:

```cpp
if (x == 5);
{ y = 3; }
```

This looks like an error, and it almost certainly is. The ; in the first line is not supposed to be there. But, unfortunately, this is a legal construct in C++. It is called an empty statement, a statement doing nothing. An empty statement before a semicolon is rarely useful. In this case, it has the unfortunate consequence of allowing what is almost certainly an error to be acceptable to the compiler, so it will not alert you to the error and you will have that much more difficulty finding it.

What will happen if this code is run? The compiler will test x to see if it has the value 5. If this condition is true, the following statement (the empty statement) will be executed, with no effect. Then the program continues to the next line, assigning the value 3 to y (which is what you wanted to have happen if x equals 5). If, on the other hand, x does not have the value 5, the compiler will not execute the empty statement (still no effect) and will continue as before to assign the value 3 to y (which is not what you wanted to have happen unless x equals 5). In other words, the if-statement doesn't matter; y is going to get the value 3 regardless. This is a common error for novice programmers, and it can be difficult to spot, so watch out for it.

The next section is devoted to statements used to alter the order of evaluation to allow us to express more interesting computations than those we get by just executing statements in the order in which they were written.
