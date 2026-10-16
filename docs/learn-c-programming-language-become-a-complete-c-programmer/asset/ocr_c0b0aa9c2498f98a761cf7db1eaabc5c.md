specifies that **inch** is of type **int**; that is, **inch** is an integer variable.
A *declaration* is a statement that introduces a name into the program. It specifies a type for the named entity:

+   - A *type* defines a set of possible values and a set of operations (for an object).
+   - An *object* is some memory that holds a value of some type.
+   - A *value* is a set of bits interpreted according to a type.
+   - A *variable* is a named object.

C++ offers a variety of fundamental types. For example:

```
bool // Boolean, possible values are true and false
char // character, for example, ‘a’, ‘z’, and ‘9’
int // integer, for example, 1, 42, and 1066
double // double-precision floating-point number, for example, 3.14 and 299793.0
```

Each fundamental type corresponds directly to hardware facilities and has a fixed size that determines the range of values that can be stored in it:

```
bool:
char:
int:
double:
```

A **char** variable is of the natural size to hold a character on a given machine (typically an 8-bit byte), and the sizes of other types are quoted in multiples of the size of a **char**. The size of a type is implementation-defined (i.e., it can vary among different machines) and can be obtained by the **sizeof** operator; for example, **sizeof(char)** equals **1** and **sizeof(int)** is often **4**.

The arithmetic operators can be used for appropriate combinations of these types:

# Section 2.2.2 Types, Variables, and Arithmetic 41

```
x+y // plus
+x // unary plus
x-y // minus
-x // unary minus
x*y // multiply
x/y // divide
x%y // remainder (modulus) for integers
```

So can the comparison operators:

```
x==y // equal
x!=y // not equal
x<y // less than
x>y // greater than
x<=y // less than or equal
x>=y // greater than or equal
```

In assignments and in arithmetic operations, C++ performs all meaningful conversions (§10.5.3) between the basic types so that they can be mixed freely:

```
void some_function() {
```