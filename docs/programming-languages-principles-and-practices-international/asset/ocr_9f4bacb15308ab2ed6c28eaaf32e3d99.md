# 11.1 The Algebraic Specification of Abstract Data Types

In this section, we focus on one example of an abstract data type, the complex data type, which is not a built-in data type in most programming languages. Mathematically, complex numbers are well-known objects and are extremely useful in practice, since they represent solutions to algebraic equations. A complex number is usually represented as a pair of real numbers (x, y) in Cartesian coordinates, which are conventionally written as x + iy, where i is a symbol representing the complex number √−1. x is called the “real” part, and y is called the “imaginary” part. There are also other ways to represent complex numbers—for example, as polar coordinates (r,u). In defining complex numbers, however, we shouldn’t need to specify their representation, but only the operations that apply to them. These include the usual arithmetic operations +, –, *, and /. We also need a way to create a complex number from a real and imaginary part, as well as functions to extract the real and imaginary parts from an existing complex number.

A general specification of a data type must include the name of the type and the names of the operations, including a specification of their parameters and returned values. This is the syntactic specification of an abstract data type and is often also called the signature of the type. In a language-independent specification, it is appropriate to use the function notation of mathematics for the operations of the data type: Given a function f from set X to set Y, X is the domain, Y is the range, and we write f: X → Y. Thus, a signature for the complex data type looks like this:

```
type complex imports real

operations:
  +: complex × complex → complex
  -: complex × complex → complex
  *: complex × complex → complex
  /: complex × complex → complex
  -: complex → complex
  makecomplex: real × real → complex
  realpart: complex → real
  imaginarypart: complex → real
```

Note that the dependence of the complex data type on an already existing data type, namely, real, is made explicit by the “imports real” clause. (Do not confuse this imports clause with the import statement in some languages.) Note also that the negative sign is used for both subtraction and negation, which are two different operations. Indeed, the usual names or symbols are used for all the arithmetic operations. Some means must eventually be used to distinguish these from the arithmetic operations on the integers and reals (or they must be allowed to be overloaded, as some languages provide).

The preceding specification lacks any notion of semantics, or the properties that the operations must actually possess. For example, z * w might be defined to be always 0! In mathematics, the semantic properties of functions are often described by equations or axioms. In the case of arithmetic operations, examples of axioms are the associative, commutative, and distributive laws. In the equations that follow, x, y, and z are assumed to be variables of type complex; that is, they can take on any complex value.

```
x + (y + z) = (x + y) + z   (associativity of +)
x * y = y * x   (commutativity of *)
x * (y + z) = x * y + x * z   (distributivity of * over +)
```