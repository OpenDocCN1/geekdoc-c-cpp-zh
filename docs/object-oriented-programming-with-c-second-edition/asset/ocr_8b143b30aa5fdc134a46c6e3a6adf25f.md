# Operator Overloading, Type Conversion, New Style Casts, RTTI 215

The benefit of overloading the operator will not be felt if the overloaded operators are directly called in this manner. (In that case, they can be well replaced by member functions.) Moreover, we must note that the name of the operator-overloading function is unusual (it contains the keyword operator). Otherwise, the operator-overloading functions are implemented just like member function, non-member, or friend functions.

# Concept of overload using friend functions

We might wonder why friend functions serve to use overloaded operators. After all, member functions serve the purpose. In order to understand this, let consider two classes A (which we have defined) and B (an existing class or an intrinsic data type). We realize that for some reason only an object of class A will be added to an object of class B to get another object of class A. This will be done as follows.

```
a2 = b1 + a1;
// a2 are objects of class A, b1 is
// an object of class B
```

An object of B will not be added to an object of class A. Objects of class B will appear on the left of the addition operator and not on the right. We will soon realize that such restrictions can and do exist. Statements such as the one below will not written.

```
a2 = b1 + a1;
// a2 are objects of class A, b1 is
// an object of class B
```

Further us assume (rather accept) that we have no means of modifying the definition of class B. (This is a perfectly acceptable restriction. We cannot define somebody's class definition. Definitions are provided in read-only header files and definitions of member functions in libraries.) Now, if we define the operator-overloading function as a member function of class A as follows, the first of the preceding statements will not compile.

```
class A
{
public:
    operator + (const B&);
};
```

The compiler will interpret the statement

```
a2 = b1 + a1;
```

first as

```
a2 = b1.operator + (a1);
```

and then as

```
a2 = operator + (b1,a1);
```

The prototype of the member function satisfies neither of these two interpretations. The compiler will naturally throw an error. Declaring the operator-overloading function as a friend function with an object of class B as the first formal argument solves the problem. See Listing 8.3.

**Listing 8.3** Operator overloading using friend function

```
class A
{
public:
```