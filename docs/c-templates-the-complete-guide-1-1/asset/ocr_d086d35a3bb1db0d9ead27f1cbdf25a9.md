somewhere in the program that causes the entity to be needed for straightforward code generation.³ The reference can be an access to the value of a variable, a call to a function, or the address of such an entity. This reference can be explicit in the source, or it can be implicit. For example, a new-expression may create and implicitly add to the associated delete operator to handle situations when a constructor throws an exception requiring the unnamed (but allocated) memory to be cleaned up. Another example consists of copy constructors, which must be defined even if they end up being optimized away (unless the language requires them to be optimized away, which is frequently the case in C++). Virtual functions are also implicitly used (by the internal constructor that enable virtual function calls), unless they are pure virtual functions. Several other kinds of implicit uses exist, but we center them for the sake of researchers.

Some references do not constitute as uses in the previous sense: Those that appear in an unevaluated operand (e.g., the operand of a sizeof or decltype operator). The example of `t` is `decltype (t)`, which is not considered only in some cases. Specifically, if a reference appears as part of a typeid operator, it is not a use in the previous sense, unless the argument of the typeid operator ends up designating a polymorphic object (an object with possibly-inherited—virtual functions). For example, consider the following single-file program:

Click here to view code image

```
```cpp
#include <typeinfo>

class Decoder
{
#if defined(FDECODER)
    virtual ~Decoder();
#endif
};

extern Decoder d;

int main()
{
    char const* name = typeid(d).name();
    return (int)strlen(name);
}
```
```

This is a valid program if and only if the purpose of typeid is not defined. Indeed, the variable d is not defined, but the reference to it in typeid(d) is not a use, and therefore no definition is needed. The reference to typeid(d) is only if d is an object of a polymorphic type (because, in general, it is always possible to determine the result of a polymorphic typeid operator until run-time).

According to the C++ standard, the constraints described in this section do not require a diagnostic from a C++ implementation. In practice, they are often reported by linters or diagnosis of missing definitions.

# A.3.2 One-per-Translation Unit Constraints

No entity can be defined more than once in a translation unit. So the following example is invalid C++:

Click here to view code image

```
```cpp
inline void f() {}
inline void f() {} // ERROR: duplicate definition
```
```

This is one of the main reasons for surrounding the code in header files with guards:

```
```cpp
#ifndef __GUARDNAME_HPP
#define __GUARDNAME_HPP

...

#endif // __GUARDNAME_HPP
```
```

Such guards ensure that the second time a header file is included, its contents are discarded, thereby avoiding the duplicate definition of a class, inline variable, method, and so on, that it may contain.

The ODR also specifies that certain entities must be defined in certain circumstances. This can be the case for class types, inline functions, and inline variables. In the following few paragraphs, we review the detailed rules.

+   A class type `x` (including structs and unions) must be defined as a translation unit prior to any of the following kinds of uses in that translation unit:
+   
+   - The creation of an object of type `x` (e.g., as a variable declaration or through a new expression). The creation could be indirect, for example, when an object that itself contains an object of type `x` is being created.
+   - The declaration of a data member of type `x`.
+   - Applying the `sizeof` or `typeid` operator on object of type `x`.
+   - Explicitly or implicitly accessing members of type `x`.
+   - Converting an expression to or from type `x` using any kind of conversion, or converting an expression to or from a pointer or reference to `x` (except `void*`) using an implicit cast, `static_cast`, or `dynamic_cast`.
+   - Assigning a value to an object of type `x`.
+   - Defining or calling a function with an argument or return type of `x`.

Just declaring such a function doesn't need the type to be defined, how-