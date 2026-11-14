
## Appendix C

### Language Definitions

> "Language is a tool adequate to
> provide any degree of precision
> relevant to a particular situation."

> —Kenneth L. Pike

This appendix is intended as a reference for definitions relevant to this book.

### C.1 Value Categories

C++ distinguishes between different categories of values. We focus here on lvalues and rvalues and have adapted the definitions from the ISO standard [38] accordingly.

**Definition C-1. (lvalue).** An _lvalue_ is an object, bit-field, function.

More pragmatically, an lvalue is or refers to an entity that has a name which allows us to determine its address with the address operator `&`. This rule is more generally applicable than we might think. Even a function whose code is substituted for each call of it and whose symbol might not even appear in the executable has an address. We can pass this function as a parameter to another function by taking its address or rely on the implicit conversion of a function into a pointer to itself. The counterpart is:

**Definition C-2. (rvalue).** An _rvalue_ is an expiring value (e.g., an object casted to an rvalue), a temporary object or sub-object thereof, or a value that is not associated with an object.

- 1. Especially with optimization and when the function is declared `inline`.

Again, we can take the pragmatic approach and say that rvalues are entities without a name and for which the address operator `&` is not allowed. This applies to all function results that are not references. Tricky are named rvalue references: they only accept rvalues but are lvalues themselves. This is particularly evident for rvalue function parameters. We can only pass rvalues to those parameters but inside the function they are lvalues and we must apply `move` or `forward` to pass them as rvalues to another function.

The historical motivation for these names is that only lvalues can appear on the left-hand side of an assignment and rvalues can only be on its right-hand side. This criterion is unfortunately not really useful since lvalues can be constant which forbids them to be on the left-hand side of an assignment. We can also assign a value to an rvalue object of a user type when the assignment operator is not qualified with an `&`; see Section 2.6.4. And lvalues are obviously allowed on the assignment's right-hand side, too.

**Definition C-3. (xvalue).** An xvalue is an lvalue that was casted to an rvalue.

While being an rvalue the object's content might be corrupted so that it is treated as expired. As we discussed in Section 2.3.5.4, properly emptied rvalue objects do not cause this problem—not even later as lvalues—and we hope that xvalue will be a term that does not matter anymore at some point in the future. For your own projects, you should use the techniques from this book and avoid corrupted data even in the presence of `std::move` and `std::forward`.

### C.2 Operator Overview

**Table C-1: Operator Summary**

| Description | Notation | Assoc. |
|---|---|---|
| Parenthesized expression | `( expr )` | - |
| Lambda | `[capture list] lambda declarator { stmt list }` | - |
| Scope resolution | `class name :: member` | - |
| Scope resolution | `namespace name :: member` | - |
| Global namespace | `:: name` | - |
| Global namespace | `:: qualified-name` | - |
| Member selection | `object . member` | ⇒ |
| Dereferenced member selection | `pointer -> member` | ⇒ |
| Subscripting | `expr [ expr ]` | ⇒ |
| Subscripting (user-defined) | `object [ expr ]` | ⇒ |
| Function call | `expr ( expr list )` | ⇒ |
| | `expr ( expr list )` | ⇒ |
| Value construction | `type ( expr list )` | ⇒ |
| | `expr ( expr list )` | - |
| Post-increment | `lvalue ++` | - |
| Post-decrement | `lvalue --` | - |
| Type identification | `typeid ( type )` | - |
| Run-time identification | `typeid ( expr )` | - |
| Run-time conversion | `checked dynamic_cast < type > ( expr )` | - |
| Compile-time checked conversion | `static_cast < type > ( expr )` | - |
| Unchecked conversion | `reinterpret_cast < type > ( expr )` | - |
| `const` conversion | `const_cast < type > ( expr )` | - |
| Size of object | `sizeof expr` | - |
| Size of type | `sizeof ( type )` | - |
| Number of arguments | `sizeof... ( argumentpack )` | - |
| Number of type arguments | `sizeof... ( typepack )` | - |
| Alignment | `alignof ( expr )` | - |
| Alignment of type | `alignof ( type )` | - |
| Pre-increment | `++ lvalue` | - |
| Pre-decrement | `-- lvalue` | - |
| Complement | `~ expr` | ⇐ |
| Not | `! expr` | ⇐ |
| Unary minus | `- expr` | ⇐ |
| Unary plus | `+ expr` | ⇐ |
| Address of | `& lvalue` | - |
| Dereference | `* expr` | ⇐ |
| Create (allocate) | `new type` | - |
| Create (allocate and initialize) | `new type ( expr list )` | - |
| Create (place) | `new ( expr list ) type` | - |
| Create (place and initialize) | `new ( expr list ) type ( expr list )` | - |
| Destroy (deallocate) | `delete pointer` | - |
| Destroy array | `delete [] pointer` | - |
| C-style cast | `( type ) expr` | <= |
| Await an exception | `co_await expr` | - |
| Member selection | `object .* pointer to member` | => |
| Member selection | `pointer ->* pointer to member` | => |
| Multiply | `expr * expr` | => |
| Divide | `expr / expr` | => |
| Modulo (remainder) | `expr % expr` | => |
| Add (plus) | `expr + expr` | => |
| Subtract (minus) | `expr - expr` | => |
| Shift left | `expr << expr` | => |
| Shift right | `expr >> expr` | => |
| Three-way comparison | `expr <=> expr` | => |
| Less than | `expr < expr` | => |
| Less than or equal | `expr <= expr` | => |
| Greater than | `expr > expr` | => |
| Greater than or equal | `expr >= expr` | => |
| Equal | `expr == expr` | => |
| Not equal | `expr != expr` | => |
| Bitwise AND | `expr & expr` | => |
| Bitwise exclusive OR (XOR) | `expr ^ expr` | => |
| Bitwise inclusive OR | `expr | expr` | => |
| Logical AND | `expr && expr` | => |
| Logical OR | `expr || expr` | => |
| Conditional expression | `expr ? expr : expr` | <= |
| Simple assignment | `lvalue = expr` | <= |
| Multiply and assign | `lvalue *= expr` | <= |
| Divide and assign | `lvalue /= expr` | <= |
| Modulo and assign | `lvalue %= expr` | <= |
| Add and assign | `lvalue += expr` | <= |
| Subtract and assign | `lvalue -= expr` | <= |
| Shift left and assign | `lvalue <<= expr` | <= |
| Shift right and assign | `lvalue >>= expr` | <= |
| Bitwise AND and assign | `lvalue &= expr` | <= |
| Bitwise inclusive OR and assign | `lvalue |= expr` | <= |
| Bitwise exclusive OR and assign | `lvalue ^= expr` | <= |
| Throw an exception | `throw expr` | - |
| Yield an exception | `co_yield expr` | - |
| Comma (sequencing) | `expr , expr` | => |

The table is an updated version of [62, §10.3],² we provided the associativity of the binary and ternary operators. Unary operators of the same priority are evaluated from inside out. In expressions with left-associative operators (marked by =>), the left sub-expression is evaluated first; for instance:

```
a + b + c + d + e // Corresponds to:
((a + b) + c) + d) + e
```

- 2. On cppreference.com, the conditional expression has the same priority as the following group with the assignments (which certainly made no difference in practice). The standard document itself doesn't provide the precedence directly as a list.

Assignments are right-associative (=); that is:

```
a = b = c = d = e // Corresponds to:
a = (b = (c = (d = e)))
```

A noteworthy detail is the definition of sizeof. It can be applied directly to expressions like objects but needs parentheses when applied to a type:

```
int i;
sizeof i;       // Okay: i is an expression
sizeof(i);      // Okay as well: extra () do not harm
sizeof int;     // Error: parentheses needed for types
sizeof(int);    // Okay
```

If you're uncertain whether parentheses are needed, you can always add some extra ones.

### C.3 Conversion Rules

Integer, floating-point, and bool values can be freely mixed in C++ as each of these types can be converted to any other. Wherever possible, values are converted such that no information is lost. A conversion is Value-Preserving when the conversion back to the original type yields the original value. Otherwise the conversion is Narrowing. This paragraph is the short version of [62, Intro §10.5].

#### C.3.1 Promotion

An implicit conversion that preserves the value is referred to as Promotion. Short integral or floating-point values can be converted exactly to longer
