using the notation

```
T x {v};
```

then you can create an object with the same value as an expression using T{v} or new T{v}. Using new places the object on the free store and returns a pointer to it, whereas “plain T{v}” makes a temporary object in the local scope (§6.4.2). For example:

```
struct S { int a, b; };

void f()
{
S v {7,8}; // direct initialization of a variable
v = S{7,8}; // assign using qualified list
S* p = new S{7,8}; // constructon free store using qualified list
}
```

The rules constructing an object using a qualified list are those of direct initialization (§16.2.6). One way of looking at a qualified initializer list with one element is as a conversion from one type to another. For example:

```
template<class T>
T square(T x)
{
return x*x; }

void f(int i) {
double d = square(double{i});
complex<double> z = square(complex<double>{i});
}
```

That idea is explored further in §11.5.1.

# 11.3.3 Unqualified Lists

A unqualified list is used where an expected type is unambiguously known. It can be used as an expression only as:

+   - A function argument
+   - A return value
+   - The right-hand operand of an assignment operator (=, +=, *=, etc.)
+   - A subscript

For example:

```
int f(double d, Matrix& m)
{
int v {7}; // initializer (direct initialization) int v2 = {7}; // initializer (copyinitialization)
int v3 = m[{2,3}]; // assume m takes value pairs as subscripts

v = {8}; // right-hand operand of assignment
v += {88}; // right-hand operand of assignment
{v} = 9; // error :not left-hand operand of assignment
v = 7+{10}; // error :not an operand of a non-assignment operator
```