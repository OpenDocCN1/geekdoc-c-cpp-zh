In this section, we consider type checking of expressions. The rules for checking statements are similar to those for expressions. For example, we treat the conditional statement “if (E) S;” as if it were the application of a function *f* to *E* and *S*. Let the special type *void* denote the absence of a value. Then function *f* is expected to be applied to a *boolean* and a *void*; the result of the application is a *void*.

# ## 6.5.2 Type Conversions

Consider expressions like *x + i*, where *x* is of type *float* and *i* is of type *integer*. Since the representation of integers and floating-point numbers is different within a computer and different machine instructions are used for operations on integers and floats, the compiler may need to convert one of the operands of + to ensure that both operands are of the same type when the addition occurs.

Suppose that integers are converted to floats when necessary, using a unary operator *(float)*. For example, the integer 2 is converted to a float in the code for the expression 2 * 3.14:

```
t₁ = (float) 2
t₂ = t₁ * 3.14
```

We can extend such examples to consider integer and float versions of the operators; for example, *int* for integer operands and *float* for floats.

Type synthesis will be illustrated by extending the scheme in Section 6.4.2 for translating expressions. We introduce another attribute *E.type*, whose value is either *integer* or *float*. The rule associated with E → E₁ + E₂ builds on the pseudocode

```
if (E₁.type = integer and E₂.type = integer)  E.type = integer;
else if (E₁.type = float and E₂.type = integer)  ⋯
⋯
```

As the number of types subject to conversion increases, the number of cases increases rapidly. Therefore with large numbers of types, careful organization of the semantic actions becomes important.

Type conversion rules vary from language to language. The rules for Java in Fig. 6.25 distinguish between *widening* conversions, which are intended to preserve information, and *narrowing* conversions, which can lose information. The widening rules are given by the hierarchy in Fig. 6.25(a): any type lower in the hierarchy can be widened to a higher type. Thus, a *char* can be widened to an *int* or a *float*, but a *char* cannot be widened to a *short*. The narrowing rules are illustrated by the graph in Fig. 6.25(b): a type *s* can be narrowed to a type *t* if there is a path from *s* to *t*. Note that *char*, *short*, and *byte* are pairwise convertible to each other.

Conversion from one type to another is said to be *implicit* if it is done automatically by the compiler. Implicit type conversions, also called *coercions*,