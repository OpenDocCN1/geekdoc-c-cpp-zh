either.) One of the problems with string literals is that two identical literals can be stored at two distinct addresses. An alternative (but cumbersome) way to express templates instantiated over constant strings involves introducing an additional variable to hold the string: Click here to view code image

```
template<char const* str>
class Message {
...;
};

extern char const hello[] = "Hello World!";
char const hello11[] = "Hello World!";

void foo()
{
static char const hello17[] = "Hello World!";

Message<hello> msg03; // OK in all versions
Message<hello11> msg11; // OK since C++11
Message<hello17> msg17; // OK since C++17
}
```

The requirement is that a nontype template parameter declared as reference or pointer can be a constant expression with external linkage in all C++ versions, internal linkage since C++11, or any linkage since C++17.

See Section 17.2 on page 354 for a discussion of possible future changes in this area Here are a few other (less surprising) invalid examples: Click here to view code image

```
template<typename T, T nontypeParam>
class C;

struct Base {
int i;
} base;

struct Derived : public Base {
} derived;

C<Base*, &derived>* err1; // ERROR: derived-to-base conversions are not considered

C<int&, base.i>* err2; // ERROR: fields of variables aren’t considered to be variables

int a[10];
C<int*, &a[0]>* err3; // ERROR: addresses of array elements aren’t acceptable either
```