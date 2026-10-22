
We also think it’s a good habit to handle the terms carefully when exchanging ideas about C and C++. We do so throughout this book.

Some constructs (such as `static_assert`) do not introduce any names but are syntactically treated as declarations.

Various optimization techniques may cause this need to be removed, but the language doesn’t assume such optimizations.

Version 1 of the gcc compiler actually jokingly did this by starting the game of Rogue in some situations like this.

Occasionally, conditional compilation directives evaluate differently in different translation units. Use such directives with care. Other differences are possible too, but they are even less common.

## Appendix B

## Value Categories

Expressions are a cornerstone of the C++ language, providing the primary mechanism by which it can express computations. Every expression has a type, which describes the static type of the value that its computation produces. The expression 7 has type int, as does the expression 5 + 2, and the expression x if x is a variable of type int. Each expression also has a value category, which describes something about how the value was formed and affects how the expression behaves.

### B.1 Traditional Lvalues and Rvalues

Historically, there were only two value categories: lvalues and rvalues. Lvalues are expressions that refer to actual values stored in memory or in a machine register, such as the expression x where x is the name of a variable. These expressions may be modifiable, allowing one to update the stored value. For example, if x is a variable of type int, the following assignment will replace the value of x with 7: x = 7;

The term lvalue is derived from the role these expressions could play within an assignment: The letter “l” stands for “left-hand side” because (historically, in C) only lvalues may occur on the left-hand side of the assignment. Conversely, rvalues (where “r” stands for “right-hand side”) could occur only on the right-hand side of an assignment expression.

However, when C was standardized in 1989, things changed: While an int const still was a value stored in memory, it could not occur on the left-hand side of an assignment:

```
int const x; // x is a nonmodifiable lvalue
x = 7; // ERROR: modifiable lvalue required on the left
```

C++ changed things even further: Class rvalues can occur on the left-hand side of assignments. Such assignments are actually function calls to the appropriate assignment operator of the class rather than “simple” assignments for scalar

types, so they follow the (separate) rules of member function calls.

Because of all these changes, the term *lvalue* is now sometimes said to stand for *localizable value*. Expressions that refer to a variable are not the only kind of lvalue expression. Another class of expressions that are lvalues include pointer dereference operations (e.g., `*p`), which refer to the value stored at the address the pointer references, and expressions that refer to a member of a class object (e.g., `p->data`). Even calls to functions that return values of “traditional” lvalue reference type declared with `&` are lvalues. For example (see Section B.4 on page 679 for details):

```
std::vector<int> v;
v.front() //yields an lvalue because the return type is an lvalue
         //reference
```

Perhaps surprisingly, string literals are also (nonmodifiable) lvalues.

Rvalues are pure mathematical values (such as 7 or the character ’a’) that don’t necessarily have any associated storage; they come into existence for the purpose of a computation but cannot be referenced again once they have been used. In particular, any literal value except string literals (e.g., 7, ’a’, `true`, `nullptr`) are rvalues, as are the results of many built-in arithmetic computations (e.g., `x + 5` for x of integer type) and calls to functions that return a result by value. That is, all temporaries are rvalues. (That doesn’t apply to named references that refer to them, though.)

### B.1.1 Lvalue-to-Rvalue Conversions

Due to their ephemeral nature, rvalues are necessarily restricted to the right-hand side of a (“simple”) assignment: An assignment `7 = 8` doesn’t make sense because the mathematical 7 isn’t allowed to be redefined. Lvalues, on the other hand, don’t appear to have the same restriction: One can certainly compute the assignment `x = y` when x and y are variables of compatible type, even though the expressions x and y are both lvalues.

The assignment `x = y` works because the expression on the right-hand side, y, undergoes an implicit conversion called the *lvalue-to-rvalue conversion*. As its name implies, the lvalue-to-rvalue conversion takes an lvalue and produces an rvalue of the same type by reading from the storage or register associated with the lvalue. This conversion therefore accomplishes two things: First, it ensures that an lvalue can be used wherever an rvalue is expected (e.g., as the right-hand side of an assignment or in a mathematical expression such as x + y). Second, it identifies where in the program the compiler (prior to optimization) may emit a “load” instruction to read a value from memory.

### B.2 Value Categories Since C++11

When rvalue references were introduced in C++11 in support of move semantics, the traditional partitioning of expressions into lvalues and rvalues was no longer sufficient to describe all the C++11 language behaviors. The C++ standardization committee therefore redesigned the value category system based on three core and two composite categories (see Figure B.1). The core categories are: *lvalue*, *prvalue* (“pure rvalue”), and *xvalue*. The composite categories are: *glvalue* (“generalized lvalue,” which is the union of *lvalue* and *xvalue*) and *rvalue* (the union of *xvalue* and *prvalue*).

Note that all expressions are still either lvalues or rvalues, but the rvalues category is now further subdivided.

![](img/0d5072d8203dcaf6ef50e76a3d9a3203_780_0.png)

- This C++11 categorization has remained in effect, but in C++17 the characterization of the categories were reformulated as follows:
  - A *glvalue* is an expression whose evaluation determines the identity of an object, bit-field, or function (i.e., an entity that has storage).
  - A *prvalue* is an expression whose evaluation initializes an object or a bit-field, or computes the value of the operand of an operator.
  - An *xvalue* is a glvalue designating an object or bit-field whose resources can be reused (usually because it is about to “expire”—the “x” in *xvalue* originally came from “eXpiring value”).
  - An *lvalue* is a glvalue that is not an xvalue.
  - An *rvalue* is an expression that is either a prvalue or an xvalue.

Note that in C++17 (and to some extent, in C++11 and C++14), the *glvalue* vs. *prvalue* dichotomy is arguably more fundamental than the traditional *lvalue* vs. *rvalue* distinction.

Although this describes the characterization introduced in C++17, those descriptions also apply to C++11 and C++14 (the prior descriptions were equivalent but harder to reason about).

Except for bit fields, glvalues produce entities with an address. That address may be that of a subobject of a larger enclosing object. In the case of a base class subobject, the type of the glvalue (expression) is called its *static type*, and the type of the most derived object that base class is part of is called the *dynamic type* of the glvalue. If the glvalue does not produce a base class subobject, its static and dynamic types are identical (i.e., the type of the expression).

Examples of *lvalues* are:
- Expressions that designate variables or functions
- Applications of the built-in unary * operator (“pointer indirection”)
- An expression that is just a string literal
- A call to a function with a return type that is an lvalue reference

Examples of *prvalues* are:
- Expressions that consist of a literal that is not a string literal or a user-defined literal¹
- Applications of the built-in unary & operator (i.e., taking the address of an expression)
- Applications of built-in arithmetic operators
- A call to a function with a return type that is *not* a reference type
- Lambda expressions

Examples of *xvalues* are:
- A call to a function with a return type that is an rvalue reference to an object type (e.g., `std::move()`)
- A cast to an rvalue reference to an object type

Note that rvalue references to function types produce lvalues, not xvalues.

It’s worth emphasizing that glvalues, prvalues, xvalues, and so on, are *expressions*, and *not* values² or entities. For example, a variable is not an lvalue even though an expression denoting a variable is an lvalue:

```
int x = 3; // x here is a variable, not an lvalue. 3 is a prvalue initializing
// the variable x.
int y = x; // x here is an lvalue. The evaluation of that lvalue expression does not
// produce the value 3, but a designation of an object containing the value 3.
// That lvalue is then then converted to a prvalue, which is what initializes y.
```

### B.2.1 Temporary Materialization

We previously mentioned that lvalues often undergo an lvalue-to-rvalue conversion³ because prvalues are the kinds of expressions that initialize objects (or provide the operands for most built-in operators).

In C++17, there is a dual to this conversion, known as *temporary*
