```
void* my_allocator(size_t);
void f() {
int* p = static_cast<int*>(my_allocator(100)); // newallocation used as ints // ...
}
```

A compiler does not know the type of the object pointed to by the void*.
The fundamental idea behind the named casts is to make type conversion more visible and to allow the programmer to express the intent of a cast:

+   - static_cast converts between related types such as one pointer type to another in the same class hierarchy, an integral type to an enumeration, or a floating-point type to an integral type. It also does conversions defined by constructors (§16.2.6, §18.3.3, §iso.5.2.9) and conversion operators (§18.4).
+   - reinterpret_cast handles conversions between unrelated types such as an integer to a pointer or a pointer to an unrelated pointer type (§iso.5.2.10).
+   - const_cast converts between types that differ only in const and volatile qualifiers (§iso.5.2.11).
+   - dynamic_cast does run-time checked conversion of pointers and references into a class hierarchy (§22.2.1, §iso.5.2.7).

These distinctions among the named casts allow the compiler to apply some minimal type checking and make it easier for a programmer to find the more dangerous conversions represented as reinterpret_casts. Some static_casts are portable, but few reinterpret_casts are. Hardly any guarantees are made for reinterpret_cast, but generally it produces a value of a new type that has the same bit pattern as its argument. If the target has at least as many bits as the original value, we can reinterpret_cast the result back to its original type and use it. The result of a reinterpret_cast is guaranteed to be usable only if its result is converted back to the exact original type. Note that reinterpret_cast is the kind of conversion that must be used for pointers to functions (§12.5). Consider:

```
char x = ‘a’;
int* p1 = &x; // error :no implicit char* to int* conversion
int* p2 = static_cast<int*>(&x); // error :no implicit char* to int* conversion
int* p3 = reinterpret_cast<int*>(&x); // OK: on your head be it
struct B { /*...*/ };
struct D : B { /*...*/ }; // see §3.2.2 and §20.5.2
B * pb = new D; // OK: implicit conversion from D* to B* D* pd = pb; // error :no implicit conversion from B* to D* D* pd = static_cast<D*>(pb); // OK
```

Conversions among class pointers and among class reference types are discussed in §22.2. If you feel tempted to use an explicit type conversion, take the time to consider if it is really necessary. In C++, explicit type conversion is unnecessary in most cases when C needs it (§1.3.3) and also in many cases in which earlier versions of C++ needed it (§1.3.2, §44.2.3). In many programs, explicit type conversion can be completely avoided; in others, its use can be localized to a