
auto c4 = narrow_cast<char>(i); // may throw
auto f2 = narrow_cast<float>(d); // may throw
auto p1 = narrow_cast<char*>(i); // compile-time error
auto i1 = narrow_cast<int>(p); // compile-time error
auto d2 = narrow_cast<double>(i);
auto i2 = narrow_cast<int>(d);
// may throw (but probably will not)
// may throw

Depending on your use of floating-point numbers, it may be worthwhile to use a range test for floating-point conversions, rather than !=. That is easily done using specializations (§25.3.4.1) or type traits (§35.4.1).

## 11.5.1 Construction

The construction of a value of type T from a value e can be expressed by the notation T{e} (§iso.8.5.4). For example:

```
auto d1 = double{2}; // d1==2.0
double d2 {double{2}/4}; // d1==0.5
```

Part of the attraction of the T{v} notation is that it will perform only “well-behaved” conversions. For example:

```
void f(int);
void f(double);

void g(int i, double d) {
f(i); // call f(int)
f(double{}); // error :{} doesn’t do int to floating conversion

f(d); // call f(double)
f(int{d}); // error :{} doesn’t truncate
f(static_cast<int>(d)); // call f(int) with a truncated value

f(round(d)); // call f(double) with a rounded value
f(static_cast<int>(lround(d))); // call f(int) with a rounded value
// if the d is overflows the int, this still truncates
}
```

I don’t consider truncation of floating-point numbers (e.g., 7.9 to 7) “well behaved,” so having to be explicit when you want it is a good thing. If rounding is desirable, we can use the standard library function round(); it performs “conventional 4/5 rounding,” such as 7.9 to 8 and 7.4 to 7.

It sometimes comes as a surprise that {}-construction doesn’t allow int to double conversion, but if (as is not uncommon) the size of an int is the same as the size of a double, then some such conversions must lose information. Consider:

```
static_assert(sizeof(int)==sizeof(double),"unexpected sizes");
int x = numeric_limits<int>::max(); // largest possible integer
double d = x;
int y = x;
```

We will not get x==y. However, we can still initialize a double with an integer literal that can be represented exactly. For example:

```
double d { 1234 }; // fine
```

Explicit qualification with the desired type does not enable ill-behaved conversions. For example:

```
void g2(char * p) {
int x = int{p}; using Pint = int*; int* p2 = Pint{p}; // ...
}
```

```
// error :no char* to int conversion
// error :no char* to int* conversion
```

For T{v}, “reasonably well behaved” is defined as having a “non-narrowing” (§10.5) conversion from v to T or having an appropriate constructor for T (§17.3).

The constructor notation T{} is used to express the default value of type T. For example:

```
template<class T> void f(const T&);
```

```
void g3() {
f(int{}); // default int value
f(complex<double>{}); // default complex value
// ...
}
```

The value of an explicit use of the constructor for a built-in type is 0 converted to that type (§6.3.5). Thus, int{} is another way of writing 0. For a user-defined type T, T{} is defined by the default constructor (§3.2.1.1, §17.6), if any, otherwise by default construction, MT{}, of each member.

Explicitly constructed unnamed objects are temporary objects, and (unless bound to a reference) their lifetime is limited to the full expression in which they are used (§6.4.2). In this, they differ from unnamed objects created using new (§11.2).

## 11.5.2 Named Casts

Some type conversions are not well behaved or easy to type check; they are not simple constructions of values from a well-defined set of argument values. For example:

```
IO_device * d1 = reinterpret_cast<IO_device*>(0Xff00); // device at 0Xff00
```

There is no way a compiler can know whether the integer 0Xff00 is a valid address (of an I/O device register). Consequently, the correctness of the conversions is completely in the hands of the programmer. Explicit type conversion, often called casting, is occasionally essential. However, traditionally it is seriously overused and a major source of errors.

Another classical example of the need for explicit type conversion is dealing with “raw memory,” that is, memory that holds or will hold objects of a type not known to the compiler. For example, a memory allocator (such as operator new(); §11.2.3) may return a void* pointing to newly allocated memory:

```
void* my_allocator(size_t);
void f() {
int* p = static_cast<int*>(my_allocator(100)); // new allocation used as ints
// ...
}
```

A compiler does not know the type of the object pointed to by the void*.
The fundamental idea behind the named casts is to make type conversion more visible and to allow the programmer to express the intent of a cast:

- static_cast converts between related types such as one pointer type to another in the same class hierarchy, an integral type to an enumeration, or a floating-point type to an integral type. It also does conversions defined by constructors (§16.2.6, §18.3.3, §iso.5.2.9) and conversion operators (§18.4).
- reinterpret_cast handles conversions between unrelated types such as an integer to a pointer or a pointer to an unrelated pointer type (§iso.5.2.10).
- const_cast converts between types that differ only in const and volatile qualifiers (§iso.5.2.11).
- dynamic_cast does run-time checked conversion of pointers and references into a class hierarchy (§22.2.1, §iso.5.2.7).

These distinctions among the named casts allow the compiler to apply some minimal type checking and make it easier for a programmer to find the more dangerous conversions represented as reinterpret_casts. Some static_casts are portable, but few reinterpret_casts are. Hardly any guarantees are made for reinterpret_cast, but generally it produces a value of a new type that has the same bit pattern as its argument. If the target has at least as many bits as the original value, we can reinterpret_cast the result back to its original type and use it. The result of a reinterpret_cast is guaranteed to be usable only if its result is converted back to the exact original type. Note that reinterpret_cast is the kind of conversion that must be used for pointers to functions (§12.5). Consider:

```
char x = ‘a’;
int* p1 = &x; // error :no implicit char* to int* conversion
int* p2 = static_cast<int*>(&x); // error :no implicit char* to int* conversion
int* p3 = reinterpret_cast<int*>(&x); // OK: on your head be it
struct B { /*...*/ };
struct D : B { /*...*/ }; // see §3.2.2 and §20.5.2
B * pb = new D; // OK: implicit conversion from D* to B*
D* pd = pb; // error :no implicit conversion from B* to D*
D* pd = static_cast<D*>(pb); // OK
```

Conversions among class pointers and among class reference types are discussed in §22.2. If you feel tempted to use an explicit type conversion, take the time to consider if it is really necessary. In C++, explicit type conversion is unnecessary in most cases when C needs it (§1.3.3) and also in many cases in which earlier versions of C++ needed it (§1.3.2, §44.2.3). In many programs, explicit type conversion can be completely avoided; in others, its use can be localized to a few routines.

## 11.5.3 C-Style Cast

From C, C++ inherited the notation (T)e, which performs any conversion that can be expressed as a combination of static_casts, reinterpret_casts, const_casts to make a value of type T from the expression e (§44.2.3). Unfortunately, the C-style cast can also cast from a pointer to a class to a pointer to a private base of that class. Never do that, and hope for a warning from the compiler if you do it by mistake. This C-style cast is far more dangerous than the named conversion operators because the notation is harder to spot in a large program and the kind of conversion intended by the programmer is not explicit. That is, (T)e might be doing a portable conversion between related types, a nonportable conversion between unrelated types, or removing the const modifier from a pointer type. Without knowing the exact types of T and e, you cannot tell.

## 11.5.4 Function-Style Cast

The construction of a value of type T from a value e can be expressed by the functional notation T(e). For example:

```
void f(double d)
{
int i = int(d); // truncated
complex z = complex(d); // make a complex from d
// ...
}
```

The T(e) construct is sometimes referred to as a function-style cast. Unfortunately, for a built-in type T, T(e) is equivalent to (T)e (§11.5.3). This implies that for many built-in types T(e) is not safe.

```
void f(double d, char * p)
{
int a = int(d); // truncates
int b = int(p); // not portable
// ...
}
```

Even explicit conversion of a longer integer type to a shorter (such as long to char) can result in nonportable implementation-defined behavior.
Prefer T{v} conversions for well-behaved construction and the named casts (e.g., static_cast) for other conversions.

## 11.6 Advice

- Prefer prefix ++ over suffix ++; §11.1.4.
- Use resource handles to avoid leaks, premature deletion, and double deletion; §11.2.1.
