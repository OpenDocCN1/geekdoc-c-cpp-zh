Floating-point numbers and class-type objects are not allowed as nontype template parameters:

Click here to view code image

```
template<typename T>
where are not

double precision Color<T> // allowed as non-
                           // type parameter

{

    return v1;
}
```

```
template<class-string name> // ERROR: class-type objects
are not
class MyClass
private parameters

};
```

When passing template arguments to pointers or references, the objects must not be string literals, temporaries, or data members and other sub-objects. Because these restrictions were relaxed with each and every C++ version before C++14, additional constraints apply:

+   - In C++11, the objects also had to have external linkage.
+   - In C++14, the objects also had to have external or internal linkage.

Thus, the following is not possible:

Click here to view code image

```
template<class T> name>
class MyClass

MyClass<"hello"> // ERROR: string literal "hello" not
                  // allowed
```

However there are workarounds (again depending on the C++ version):

Click here to view code image

```
extern char const s11[] = "hi";   // external linkage
char const s14[] = "hi";          // internal linkage

int main()
{
    Messenger<s3> msg;             // for all versions
    Messenger<s11> msg;            // C++11 and C++14
    Messenger<s14> msg;            // C++17 and later
}
```

In all three cases a constant character array is initialized by "hello" and this object is used as a template parameter declared with either const-, This is valid in all C++ versions if the object has external linkage (s3), in C++11 and C++14 also if it has internal linkage (s11), and since C++17 if it has no linkage at all.

See Section 3.2.3 on page 157 for a detailed discussion and Section 7.2 on page 354 for a discussion of possible future changes in this area.

# Avoiding Invalid Expressions

Arguments for nontype template parameters might be any compile-time expressions. For example:

Click here to view code image

```
template<int i, bool b>
class C;

C<sizeof(int) + 4, sizeof(int)> c;
```

However, note that if operator> is used in the expression, you have to put the whole expression into parentheses so that the nested > ends the argument list:

Click here to view code image

```
C<42, sizeof(int) > 4> c;    // ERROR: first > ends the
                                // template argument list
C<42, sizeof(int) >= 4> c;   // OK
```

# 3.4 TEMPLATE PARAMETER TYPE AUTO