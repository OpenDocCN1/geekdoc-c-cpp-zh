
Few programs are written without loops. For example, we might like to give the user a few tries to produce acceptable input:

```
bool accept3()
{
int tries = 1;
while (tries<4) {
cout << "Do you want to proceed (y or n)?\n"; char answer = 0;
cin >> answer;

// writequestion
// read answer
switch (answer) {
case 'y':
return true;

case 'n':
return false;
default:
cout << "Sorry, I don't understand that.\n"; ++tries; // increment
}
}
cout << "I'll take that for a no.\n";
return false;
}
```

The while-statement executes until its condition becomes false.

## 2.2.5 Pointers, Arrays, and Loops

An array of elements of type char can be declared like this:

```
char v[6]; // array of 6 characters
```

Similarly, a pointer can be declared like this:

```
char*p; // pointer to character
```

In declarations, [] means "array of" and * means "pointer to." All arrays have 0 as their lower bound, so v has six elements, v[0] to v[5]. The size of an array must be a constant expression (§2.2.3). A pointer variable can hold the address of an object of the appropriate type:

```
char*p = &v[3]; // p points to v's fourth element
```

```
char x = *p; // *p is the object that p points to
```

In an expression, prefix unary * means "contents of" and prefix unary & means "address of." We can represent the result of that initialized definition graphically:

p:

0: 1: 2: 3: 4: 5: v:

Consider copying ten elements from one array to another:

```
void copy_fct()
{
int v1[10] = {0,1,2,3,4,5,6,7,8,9};
int v2[10]; // to become a copy of v1
for (auto i=0; i!=10; ++i) // copy elements
v2[i]=v1[i];
// ...
}
```

This for-statement can be read as "set i to zero; while i is not 10, copy the i th element and increment i." When applied to an integer variable, the increment operator, ++, simply adds 1. C++ also offers a simpler for-statement, called a range for-statement, for loops that traverse a sequence in the simplest way:

```
void print()
{
int v[] = {0,1,2,3,4,5,6,7,8,9};
for (auto x : v) // foreach x in v
cout << x << '\n';
for (auto x : {10,21,32,43,54,65})
cout << x << '\n';
// ...
}
```

The first range for-statement can be read as "for every element of v, from the first to the last, place a copy in x and print it." Note that we don't have to specify an array bound when we initialize it with a list. The range for-statement can be used for any sequence of elements (§3.4.1).

If we didn't want to copy the values from v into the variable x, but rather just have x refer to an element, we could write:

```
void increment() {
int v[] = {0,1,2,3,4,5,6,7,8,9};
for (auto& x : v)
++x;
// ...
}
```

In a declaration, the unary suffix & means "reference to." A reference is similar to a pointer, except that you don't need to use a prefix * to access the value referred to by the reference. Also, a reference cannot be made to refer to a different object after its initialization. When used in declarations, operators (such as &, *, and []) are called declarator operators:

```
T a[n]; // T[n]: array of n Ts (§7.3)
T* p; // T*: pointer to T (§7.2)
T& r; // T&: reference to T (§7.7)
T f(A); // T(A): function taking an argument of type A returning a result of type T (§2.2.1)
```

We try to ensure that a pointer always points to an object, so that dereferencing it is valid.

When we don't have an object to point to or if we need to represent the notion of "no object available" (e.g., for an end of a list), we give the pointer the value **nullptr** ("the null pointer"). There is only one **nullptr** shared by all pointer types:

```
double * pd = nullptr;
Link<Record>* lst = nullptr; // pointer to a Link to a Record
int x = nullptr; // error: nullptr is a pointer not an integer
```

It is often wise to check that a pointer argument that is supposed to point to something, actually points to something:

```
int count_x(char * p, char x)
// count the number of occurrences of x in p[]
// p is assumed to point to a zero-terminated array of char (or to nothing)
{
if (p==nullptr) return 0; int count = 0;
for (; *p!=0; ++p)
if (*p==x)
++count; return count;
}
```

Note how we can move a pointer to point to the next element of an array using **++** and that we can leave out the initializer in a **for**-statement if we don't need it.

The definition of **count_x()** assumes that the **char*** is a C-style string, that is, that the pointer points to a zero-terminated array of **char**. In older code, **0** or **NULL** is typically used instead of **nullptr** (§7.2.2). However, using **nullptr** eliminates potential confusion between integers (such as **0** or **NULL**) and pointers (such as **nullptr**).

Section 2.3 User-Defined Types 47

## 2.3 User-Defined Types

We call the types that can be built from the fundamental types (§2.2.2), the **const** modifier (§2.2.3), and the declarator operators (§2.2.5) *built-in types*. C++'s set of built-in types and operations is rich, but deliberately low-level. They directly and efficiently reflect the capabilities of conventional computer hardware. However, they don't provide the programmer with high-level facilities to conveniently write advanced applications. Instead, C++ augments the built-in types and operations with a sophisticated set of *abstraction mechanisms* out of which programmers can build such highlevel facilities. The C++ abstraction mechanisms are primarily designed to let programmers design and implement their own types, with suitable representations and operations, and for programmers to simply and elegantly use such types. Types built out of the built-in types using C++'s abstraction mechanisms are called *user-defined types*. They are referred to as classes and enumerations. Most of this book is devoted to the design, implementation, and use of user-defined types. The rest of this chapter presents the simplest and most fundamental facilities for that. Chapter 3 is a more complete description of the abstraction mechanisms and the programming styles they support. Chapter 4 and Chapter 5 present an overview of the standard library, and since the standard library mainly consists of user-defined types, they provide examples of what can be built using the language facilities and programming techniques presented in Chapter 2 and Chapter 3.

### 2.3.1 Structures

The first step in building a new type is often to organize the elements it needs into a data structure, a struct:

```
struct Vector {
int sz; // number of elements
double* elem; // pointer to elements
};
```

This first version of Vector consists of an int and a double*.

A variable of type Vector can be defined like this:

```
Vector v;
```

However, by itself that is not of much use because v's elem pointer doesn't point to anything. To be useful, we must give v some elements to point to. For example, we can construct a Vector like this:

```
void vector_init(Vector& v, int s)
{
v.elem = new double[s]; // allocate an array of s doubles
v.sz = s;
}
```

That is, v's elem member gets a pointer produced by the new operator and v's size member gets the number of elements. The & in Vector& indicates that we pass v by nonconst reference (§2.2.5, §7.7); that way, vector_init() can modify the vector passed to it.

The new operator allocates memory from an area called the free store (also known as dynamic memory and heap; §11.2).

A simple use of Vector looks like this:

```
double read_and_sum(int s)
// read s integers from cin and return their sum; s is assumed to be positive
{
Vector v;
vector_init(v,s); // allocate s elements for v
for (int i=0; i!=s; ++i)
cin>>v.elem[i]; // read into elements

double sum = 0;
for (int i=0; i!=s; ++i)
sum+=v.elem[i]; // take the sum of the elements
return sum;
}
```

There is a long way to go before our Vector is as elegant and flexible as the standard-library vector. In particular, a user of Vector has to know every detail of Vector's representation. The rest of this chapter and the next gradually improve Vector as an example of language features and techniques. Chapter 4 presents the standard-library vector, which contains many nice improvements, and Chapter 31 presents the complete vector in the context of other standard-library facilities.

I use vector and other standard-library components as examples
- to illustrate language features and design techniques, and
- to help you learn and use the standard-library components.

Don't reinvent standard-library components, such as vector and string; use them. We use . (dot) to access struct members through a name (and through a reference) and-> to access struct members through a pointer. For example:

```
void f(Vector v, Vector& rv, Vector * pv)
{ int i1 = v.sz; int i2 = rv.sz; int i4 = pv->sz;
}
```
 // access through name // access through reference // access through pointer

### 2.3.2 Classes

Having the data specified separately from the operations on it has advantages, such as the ability to use the data in arbitrary ways. However, a tighter connection between the representation and the operations is needed for a user-defined type to have all the properties expected of a "real type." In particular, we often want to keep the representation inaccessible to users, so as to ease use, guarantee consistent use of the data, and allow us to later improve the representation. To do that we have to distinguish between the interface to a type (to be used by all) and its implementation (which has access to the otherwise inaccessible data). The language mechanism for that is called a class. A class is defined to have a set of members, which can be data, function, or type members. The interface is defined by the public members of a class, and private members are accessible only through that interface. For example:

Section 2.3.2 Classes 49

```
class Vector {
public:
Vector(int s) :elem{new double[s]}, sz{s} { } // construct a Vector
double& operator[](int i) { return elem[i]; } // element access: subscripting
int size() { return sz; }
private:
double*elem; // pointer to the elements
int sz; // the number of elements
};
```

Given that, we can define a variable of our new type Vector:

```
Vector v(6); // a Vector with 6 elements
```

We can illustrate a Vector object graphically:
