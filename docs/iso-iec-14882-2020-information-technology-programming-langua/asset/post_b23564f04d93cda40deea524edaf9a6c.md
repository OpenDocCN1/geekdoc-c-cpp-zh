
## ISO/IEC 14882:2020(E)

[Note 2: The fact that such an argument is an rvalue does not affect the ranking of implicit conversion sequences (12.4.4.3). — end note]

6 Because other than in list-initialization only one user-defined conversion is allowed in an implicit conversion sequence, special rules apply when selecting the best user-defined conversion (12.4.4, 12.4.4.2).

[Example 2:

```
class T {
public:
  T();
};

class C : T {
public:
  C(int);
};
T a = 1;            // error: no viable conversion (T(C(1)) not considered)
— end example]
```

7 In each case where a candidate is a function template, candidate function template specializations are generated using template argument deduction (13.10.4, 13.10.3). If a constructor template or conversion function template has an explicit-specifier whose constant-expression is value-dependent (13.8.3), template argument deduction is performed first and then, if the context requires a candidate that is not explicit and the generated specialization is explicit (9.2.3), it will be removed from the candidate set. Those candidates are then handled as candidate functions in the usual way.121 A given name can refer to one or more function templates and also to a set of non-template functions. In such a case, the candidate functions generated from each function template are combined with the set of non-template candidate functions.

8 A defaulted move special member function (11.4.5.3, 11.4.6) that is defined as deleted is excluded from the set of candidate functions in all contexts. A constructor inherited from class type C (11.10.4) that has a first parameter of type “reference to cv1 P” (including such a constructor instantiated from a template) is excluded from the set of candidate functions when constructing an object of type cv2 D if the argument list has exactly one argument and C is reference-related to P and P is reference-related to D.

[Example 3:

```
struct A {
  A();                                 // #1
  A(A &&);                             // #2
  template<typename T> A(T &&);        // #3
};
struct B : A {
  using A::A;
  B(const B &);                        // #4
  B(B &&) = default;                   // #5, implicitly deleted
  struct X { X(X &&) = delete; } x;
};
extern B b1;
B b2 = static_cast<B&&>(b1);           // calls #4: #1 is not viable, #2, #3, and #5 are not candidates
struct C { operator B&&() {}; };
B b3 = C();                            // calls #4
— end example]
```

## 12.4.2.2 Function call syntax [over.match.call]

### 12.4.2.2.1 General [over.match.call.general]

1 In a function call (7.6.1.3)

```
postfix-expression ( expression-list_opt )
```

> 121) The process of argument deduction fully determines the parameter types of the function template specializations, i.e., the parameters of function template specializations contain no template parameter types. Therefore, except where specified otherwise, function template specializations and non-template functions (9.3.4.6) are treated equivalently for the remainder of overload resolution.

7 The argument list contains all of the operands of the operator. The best function from the set of candidate functions is selected according to 12.4.3 and 12.4.4.125

[Example 2:

```
struct A {
    operator int();
};
A operator+(const A&, const A&);
void m() {
    A a, b;
    a + b;            // operator+(a, b) chosen over int(a) + int(b)
}
```

— end example]

8 If a rewritten operator<=> candidate is selected by overload resolution for an operator @, x @ y is interpreted as 0 @ (y <=> x) if the selected candidate is a synthesized candidate with reversed order of parameters, or (x <=> y) @ 0 otherwise, using the selected rewritten operator<=> candidate. Rewritten candidates for the operator @ are not considered in the context of the resulting expression.

9 If a rewritten operator== candidate is selected by overload resolution for an operator @, its return type shall be cv bool, and x @ y is interpreted as:

- (9.1) — if @ is != and the selected candidate is a synthesized candidate with reversed order of parameters, !(y == x),
- (9.2) — otherwise, if @ is !=, !(x == y),
- (9.3) — otherwise (when @ is ==), y == x,

in each case using the selected rewritten operator== candidate.

10 If a built-in candidate is selected by overload resolution, the operands of class type are converted to the types of the corresponding parameters of the selected operation function, except that the second standard conversion sequence of a user-defined conversion sequence (12.4.4.2.3) is not applied. Then the operator is treated as the corresponding built-in operator and interpreted according to 7.6.

[Example 3:

```
struct X {
    operator double();
};

struct Y {
    operator int*();
};

int *a = Y() + 100.0;      // error: pointer arithmetic requires integral operand
int *b = Y() + X();       // error: pointer arithmetic requires integral operand
```

— end example]

11 The second operand of operator-> is ignored in selecting an operator-> function, and is not an argument when the operator-> function is called. When operator-> returns, the operator -> is applied to the value returned, with the original second operand.126

12 If the operator is the operator ,, the unary operator &, or the operator ->, and there are no viable functions, then the operator is assumed to be the built-in operator and interpreted according to 7.6.

13 [Note 3: The lookup rules for operators in expressions are different than the lookup rules for operator function names in a function call, as shown in the following example:

```
struct A { };
void operator + (A, A);

struct B {
    void operator + (B);
}
```

```
void f ();
};

A a;

void B::f() {
    operator+ (a,a);        // error: global operator hidden by member
    a + a;                  // OK: calls global operator+
}
```

— end note]

## 12.4.2.4 Initialization by constructor [over.match.ctor]

1 When objects of class type are direct-initialized (9.4), copy-initialized from an expression of the same or a derived class type (9.4), or default-initialized (9.4), overload resolution selects the constructor. For direct-initialization or default-initialization that is not in the context of copy-initialization, the candidate functions are all the constructors of the class of the object being initialized. For copy-initialization (including default initialization in the context of copy-initialization), the candidate functions are all the converting constructors (11.4.8.2) of that class. The argument list is the expression-list or assignment-expression of the initializer.

## 12.4.2.5 Copy-initialization of class by user-defined conversion [over.match.copy]

1 Under the conditions specified in 9.4, as part of a copy-initialization of an object of class type, a user-defined conversion can be invoked to convert an initializer expression to the type of the object being initialized. Overload resolution is used to select the user-defined conversion to be invoked.

> [Note 1: The conversion performed for indirect binding to a reference to a possibly cv-qualified class type is determined in terms of a corresponding non-reference copy-initialization. — end note]

Assuming that “cv1 T” is the type of the object being initialized, with T a class type, the candidate functions are selected as follows:

- (1.1) — The converting constructors (11.4.8.2) of T are candidate functions.
- (1.2) — When the type of the initializer expression is a class type “cv S”, the non-explicit conversion functions of S and its base classes are considered. When initializing a temporary object (11.4) to be bound to the first parameter of a constructor where the parameter is of type “reference to cv2 T” and the constructor is called with a single argument in the context of direct-initialization of an object of type “cv3 T”, explicit conversion functions are also considered. Those that are not hidden within S and yield a type whose cv-unqualified version is the same type as T or is a derived class thereof are candidate functions. A call to a conversion function returning “reference to X” is a glvalue of type X, and such a conversion function is therefore considered to yield X for this process of selecting candidate functions.

2 In both cases, the argument list has one argument, which is the initializer expression.

> [Note 2: This argument will be compared against the first parameter of the constructors and against the implicit object parameter of the conversion functions. — end note]

## 12.4.2.6 Initialization by conversion function [over.match.conv]

1 Under the conditions specified in 9.4, as part of an initialization of an object of non-class type, a conversion function can be invoked to convert an initializer expression of class type to the type of the object being initialized. Overload resolution is used to select the conversion function to be invoked. Assuming that “cv1 T” is the type of the object being initialized, and “cv S” is the type of the initializer expression, with S a class type, the candidate functions are selected as follows:

- (1.1) — The conversion functions of S and its base classes are considered. Those non-explicit conversion functions that are not hidden within S and yield type T or a type that can be converted to type T via a standard conversion sequence (12.4.4.2.2) are candidate functions. For direct-initialization, those explicit conversion functions that are not hidden within S and yield type T or a type that can be converted to type T with a qualification conversion (7.3.6) are also candidate functions. Conversion functions that return a cv-qualified type are considered to yield the cv-unqualified version of that type for this process of selecting candidate functions. A call to a conversion function returning “reference to X” is a glvalue of type X, and such a conversion function is therefore considered to yield X for this process of selecting candidate functions.
