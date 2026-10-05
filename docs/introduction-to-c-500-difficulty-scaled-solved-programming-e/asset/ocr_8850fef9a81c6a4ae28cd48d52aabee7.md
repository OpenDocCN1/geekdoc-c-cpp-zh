# 484 Introduction to C++

arithmetic, relational, logical, bit, and unary increase/decrease operators are examples of expressions that produce values. An lvalue reference is not allowed to refer to the result of such expressions. In general, in such expressions we can associate a const lvalue reference or an rvalue reference. Rvalue reference is not allowed to refer to an lvalue. Let's look at some examples with lvalue and rvalue references:

```
int i;
double f() {return 1.2;}

double&& rl = f(); // Correct. The return value of f() is rvalue.
int&& rl = i; // Wrong. rl is an rvalue reference, while i is lvalue. */
double&& rl = f(); // Wrong. The return value of f() is not lvalue.
int& rl = i+10; // Wrong. The result of i+10 is rvalue.
const int& rl = i+10; // Correct. It is allowed an lvalue const reference toefer to an rvalue. /*
```

The essential difference between an lvalue and an rvalue reference is that the lvalue reference refers to an entity that will continue to exist, while the rvalue reference refers to an entity that is to be destroyed. An rvalue reference accesses the object that refers to in the same way as an lvalue reference or an ordinary variable. After all, an rvalue reference, like an lvalue reference, is a synonym of the referred variable. For example:

```
void f(string&& str)
{
    if(str[0] == 't')
    {
    }
}
f("test"); // An rvalue reference may refer to a literal string.
```

Note that if we write:

```
string s("test\nf(s); // Wrong.
```

The compiler will display an error message because an lvalue (e.g., s) cannot be associated with an rvalue reference (e.g., str).
Before ending this section, just to remind you that we use rvalue references or the move() function to perform operations on objects that we don't need their data anymore. The result is performance improvement.

# constexpr FUNCTIONS

Sometimes we want to evaluate the return value of a function (e.g., suppose that a function calculates some value) at compile time rather than performing the same evaluation over and over at runtime. That's the main idea of constexpr functions; to improve the performance of the program by performing computations at compile time rather than runtime.

Since C11, to tell the compiler that it is possible to evaluate a function at compile time we use the constexpr specifier. However, a constexpr must satisfy several requirements. For example, any given arguments must be constant expressions. Regarding its body, C++11 had posed many restrictions. For example, loops and if statements were not allowed. Fortunately, C++14 relaxes