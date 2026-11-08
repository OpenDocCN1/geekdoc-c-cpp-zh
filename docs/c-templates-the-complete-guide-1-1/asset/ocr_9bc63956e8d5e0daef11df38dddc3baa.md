erations in which that type x must be defined. These situations create a point of instantiation (POI) for x (see §4.3.5.3 on page 355).

inline functions must be defined in every translation unit in which they are used and they must be defined exactly the same way in every case. As before, whenever a function is used in multiple translation units, its definition can be different in each one:

```
```cpp
inline int length(const char* p)
{
    int ret = 0;
    // ...
    ret += strlen(p);
    return ret;
}
```
```

Although this code is valid C++, some compilers based on older technology do not actually “inline” the call. The call is a function call with a body that you cannot see, just like the definition of any out-of-line function.

Just with class templates, the use of a function generated from a non-template function declaration (a function or member function template, or a member function of a class template) creates a point of instantiation. Unlike class templates, however, the corresponding definition can appear after the point of instantiation.

The facets of the ODR explained in this subsection are generally easily verified by C++ compilers. In fact, the C++ standard requires that compilers issue diagnostics if a function is not defined in a translation unit in which it is used. An exception is the lack of diagnostics of a parameterized function. Such situations are typically not diagnosed.

# ### 3.3.3 Cross-Translation Unit Equivalence Constraints

The ability to define local entities of certain types in more than one translation unit with the potential for a one-to-one or even multiple-to-one correspondence between those entities is necessary and useful, but it also creates some potential problems in traditional compiler technology in which translation units are processed one at a time. Consequently, the C++ standard imposes a number of additional restrictions on programs. The constraints and requirements that must be satisfied by all programs are known as the one-definition rule (ODR).

The C++ standard specifies the meaning of “same entity” because of the possible ambiguity in the term. However, in this book, we use the term in the same way as the standard's definition. The C++ standard's concept of “same entity” is rather complicated, but it can be summarized as follows:

+   - The entity is defined in two different places, the two places must consist of exactly the same sequence of tokens (the keywords, operators, identifiers, and so on).
+   - The entities must correspond to the same entity. In other words, the names in the two places must denote the same entity, and the scopes in the two places must be the same. The easiest way to make sure the latter condition is satisfied is to put the entity in a header file.

Consider the following example:

```
```cpp
// --- translation unit 1:
static int counter = 0;

inline void increaseCounter()
{
    ++counter;
}
```
```

```
```cpp
// --- translation unit 2:
static int counter = 0;

inline void increaseCounter()
{
    ++counter;
}
```
```

This example is in error because even though the token sequence for the inline function increaseCounter() looks identical in both translation units, they contain a token counter that refers to two different entities. One counter has internal linkage, and the other has external linkage. The entities named counter are, therefore, not identical. Note that this is an error even though neither of the inline functions is actually used.

Pointing the definition of entities that can be defined in multiple translation units to a header file is an effective way to prevent many ODR violations. To reduce the number of additional restrictions, the standard also requires that some declarations be identical in all scopes. With this approach, structures in which two identical declarations refer to different things become fairly rare, but when this does happen, the resulting errors are often mysterious and hard to track.

The one-definition rule constraints apply not only to references that can be defined in multiple places but also to default arguments in declarations. In other words, the following program may not be identical:

```
```cpp
// --- translation unit 1:
void critical(const int& i);
void f()
{
    critical(42);
}
```
```

```
```cpp
// --- translation unit 2:
void critical(const int& i = 42);
```
```

We should note here that the equivalence of inline strings can sometimes involve multiple explicit objects. The following example is lifted (a slightly modified)