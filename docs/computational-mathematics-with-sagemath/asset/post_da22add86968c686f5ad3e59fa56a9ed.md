
## 5 Computational Domains

Writing mathematics on paper or on the blackboard requires a compromise between ease of notations and rigour. The same holds for the day-to-day use of a computer algebra system. Sage tries to give this choice to the user, by letting her/him specify, more or less rigorously, the computational domains: what is the nature of the considered objects, in which sets do they live, which operations can be applied to them?

### 5.1 Sage is Object-Oriented

Python and Sage use heavily the object-oriented programming paradigm. Even though this remains relatively transparent in common use, it is useful to know a little about this paradigm, which is quite natural in a mathematical context.

#### 5.1.1 Objects, Classes and Methods

The object-oriented programming paradigm consists in modelling each physical or abstract entity one wishes to manipulate by a programming language construction called an *object*. In most cases, as in Python, each object is an instance of a *class*. For example, the rational number 12/35 is represented by an object which is an instance of the `Rational` class:

```
sage: o = 12/35
sage: type(o)
<type 'sage.rings.rational.Rational'>
```

Note that this class is really associated to the object 12/35, and not to the variable o in which it is stored:

```
sage: type(12/35)
<type 'sage.rings.rational.Rational'>
```

Let us be more precise. An *object* is a part of the computer memory which stores the required information to represent the corresponding entity. The *class* in turn defines two things:

- 1. the *data structure* of an object, i.e., how the information is organised in memory. For example, the Rational class specifies that a rational number like 12/35 is represented by two integers: its numerator and its denominator;
- 2. its *behaviour*, in particular the available *operations* on this object: how to obtain the numerator of a rational number, how to compute its absolute value, how to multiply or add two rational numbers. Each of these operations is implemented by a *method* (here respectively `numerator`, `abs`, `__mul__`, `__add__`).

To factor an integer, we will thus call the *factor* method with the following syntax:

```
sage: o = 720
sage: o.factor()
2^4 * 3^2 * 5
```

which we can read as follows: “take the value of `o` and apply to it the *factor* method, without any other argument”. Under the hood, Python performs the following computation:

```
sage: type(o).factor(o)
2^4 * 3^2 * 5
```

From left to right: “request from the class of `o` (`type(o)`) the factorisation method (`type(o).factor`), and apply it to `o`”.

Please note that we can apply this method not only to a variable, but also directly to a value:

```
sage: 720.factor()
2^4 * 3^2 * 5
```

and thus we can chain the operations, from left to right. Here, we first take the numerator of a rational number, then we factor this numerator:

```
sage: o = 720 / 133
sage: o.numerator().factor()
2^4 * 3^2 * 5
```

To make the user’s life easier, Sage also provides a *function* `factor`, so that `factor(o)` is a shortcut for `o.factor()`. It is the case for several common functions, and it is possible to add our own shortcuts, as illustrated in the following exercise.

**Exercise 18.** Build a shortcut `ndigits` so that `ndigits(o)` calls the `ndigits` method of the object `o`.

#### 5.1.2 Objects and Polymorphism

Almost all Sage operations are *polymorphic*, i.e., they apply to several kinds of objects. For example, whatever the nature of the object `o` that we want to “factor”, we will use the same notation `o.factor()` (or its shortcut `factor(o)`). The computations to be performed however differ to factor an integer or a polynomial! They also differ if the polynomial has rational coefficients, or coefficients in a finite field. The object class determines the version of the factor code that will be called.

Similarly, like the usual mathematical notation, the product of two objects `a` and `b` can always be denoted `a*b`, even if the algorithm used differs in each case[^1]. Here is a product of two integers:

```
sage: 3 * 7
21
```

a product of two rational numbers, obtained by multiplying the numerators and denominators, then reducing the fraction:

```
sage: (2/3) * (6/5)
4/5
```

a product of two complex numbers, using the relation `i² = −1`:

```
sage: (1 + I) * (1 - I)
2
```

some commutative products of two formal expressions:

```
sage: (x + 2) * (x + 1)
(x + 2)*(x + 1)
sage: (x + 1) * (x + 2)
(x + 2)*(x + 1)
```

Apart from the notation simplicity, this form of polymorphism enables us to write *generic* programs which apply to any object having the involved operations (here multiplication):

```
sage: def fourth_power(a):
....:     a = a * a
....:     a = a * a
....:     return a
```

```
sage: fourth_power(2)
16
sage: fourth_power(3/2)
81/16
sage: fourth_power(I)
1
sage: fourth_power(x+1)
(x + 1)^4
sage: M = matrix([[0,-1],[1,0]]); M
[ 0 -1]
[ 1  0]
sage: fourth_power(M)
[1 0]
[0 1]
```

#### 5.1.3 Introspection

Python objects, and therefore Sage objects, have some *introspection* features. This means that, during execution, we can “ask” an object for its class, its methods, etc., and manipulate the obtained information using the usual constructions of the programming language. For instance, the class of an object o is itself a Python object, and we can obtain it using `type(o)`:

```
sage: t = type(5/1); t
<type 'sage.rings.rational.Rational'>
sage: t == type(5)
False
```

We see here that the expression 5/1 constructs the rational number 5, which differs — as a Python object — from the integer 5!

The introspection tools also give access to the factorisation on-line help from an object of integer type:

```
sage: o = 720
sage: o.factor?
Docstring:
    Return the prime factorization of this integer as a formal
    Factorization object.

...
```

and even to the source code of that function:

```
sage: o.factor??
...
def factor(self, algorithm='pari', proof=None, ...)
    ...
    if algorithm == 'pari':
        ...
    elif algorithm in ['kash', 'magma']:
        ...
```

Avoiding some technical details, we see here that Sage delegates the integer factorisation to other tools (PARI/GP, Kash, or Magma).

In the same vein, we can use automatic completion to interactively “ask” an object o which operations can be applied to it:

```
sage: o.<tab>
o.n	o.nbits	o.ndigits
o.next_prime	o.next_prime_power	o.next_probable_prime
o.nth_root	o.numerator	o.numerical_approx
```

Once again, it is a form of introspection.

### 5.2 Elements, Parents, Categories

#### 5.2.1 Elements and Parents

In the preceding section, we have seen the concept of *class* of an object. In practice, it is enough to know that this notion exists; we rarely have to explicitly look for the type of an object. However, Sage introduces another concept closer to mathematics: the *parent* of an object, that we will detail now.

Assume for example that we want to know if an element *a* is *invertible*. The answer does not only depend on the element itself, but also on the mathematical set *A* it belongs to (and its potential inverse). For example, the number 5 is not invertible in the set ℤ of integers, since its inverse 1/5 is not an integer:

```
sage: a = 5; a
5
sage: a.is_unit()
False
```

However, it is invertible in the set of rational numbers:

```
sage: a = 5/1; a
5
sage: a.is_unit()
True
```

Sage gives two different answers to that question since, as seen in the above section, the objects 5 and 5/1 have different classes.

In some object-oriented computer algebra systems, like MuPAD or Axiom, the mathematical set *X* to which *x* belongs (here ℤ or ℚ) is simply the class of *x*. Sage follows the approach of the Magma system, and defines the set *X* by another object attached to *x*, called its *parent*:

```
sage: parent(5)
Integer Ring
sage: parent(5/1)
Rational Field
```

We can obtain these two sets with the following shortcuts:

```
sage: ZZ
Integer Ring
```

[^1]: For a binary operation like the product, the selection of the appropriate method is slightly more complex than what was described above. Indeed, with mixed operations like the sum 2 + 3/4 of an integer and of a rational number. In this case, 2 will be converted into the rational 2/1, and the addition of two rationals will be called. The rules that describe which operand must be converted, and how it should be converted, are part of the *coercion model*.
