# ISO/IEC 14882:2017(E)

Standard, the macro invocation produces different outcomes because the single quotes delimit a character literal in C++ 2011, whereas they are digitators in this International Standard:

```
#define M(x, ...) __VAR_ARGS__\nint x[2] = {M(1,2,3, 4), 5};\n// int x[2] = { 5 }; // C++ 2011\n// int x[2] = { 3, 4, 5 }; // this International Standard:
```

# C.3.2 Basic concepts

6.7.4

Change: New usual (non-placement) deallocator.\nRationale: Required for sized deallocation.\nEffect on original feature: Valid C++ 2011 code could declare a global placement allocation function and deallocation functions follows:

```
void operator delete(size_t, std::size_t);\nvoid operator delete(void*, size_t) noexcept;
```

In this International Standard, however, the declaration of operator delete might match a predefined (non-placement) operator delete (6.7.4). If so, the program is ill-formed, as it was for class member allocation and deallocation functions (8.3.4).\nChange: A conditional expression with a throw expression as its second or third operand keeps the type and value of the other operand.\nRationale: Formally mandated conversions (Ivalue-to-reference (7.1), array-to-pointer may behave differently in this International Standard.

# C.3.3 Loop expressions

8.16

Effect on original feature: Valid C++ 2011 code that relies on the conversions may behave differently in this International Standard.

```
struct S {
  int x : 1;\n  void mf(bool cond) {\n    s;\n    (cond ? throw 0) : mf();\n    return s.x;\n  }\n}
```

In C++ 2011, it returns 1. In this International Standard, it returns 2.\nsizeof(type **) : throw 0\nIn this International Standard, the expression yields sizeof(const char*).

# C.3.4 Loop declarations

10.1.5

Change: constexpr non-static member functions are not implicitly const member functions.\nRationale: Necessary to allow member functions to mutate the object.\nEffect on original feature: Valid C++ 2011 code may fail to compile in this International Standard. For example, the following code is valid in C++ 2011 but invalid in this International Standard because it declares the same member function with different return types:

§ C.3.4

©ISO/IEC 2017 - All rights reserved 1448