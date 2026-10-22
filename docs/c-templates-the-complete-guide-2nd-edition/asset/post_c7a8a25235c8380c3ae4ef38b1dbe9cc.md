
# details/inject.cpp

```
#include <iostream>

int c;
class C {
private:
int i[2];
public:
static int f() {
return sizeof(C);
}
};

int f()
{
return sizeof(C);
}

int main()
{
std::cout << "C::f() = " << C::f() << ','
<< " ::f() = " << ::f() << '\n';
}
```

The member function C::f() returns the size of type C, whereas the function ::f() returns the size of the variable C (in other words, the size of an int object).

Class templates also have injected class names. However, they’re stranger than ordinary injected class names: They can be followed by template arguments (in which case they are injected class template names), but if they are not followed by template arguments they represent the class with its parameters as its arguments (or, for a partial specialization, its specialization arguments) if the context expects a type, or a template if the context expects a template. This explains the following situation: Click here to view code image

```
template<template<typename> class TT> class X {
};

template<typename T> class C {
C* a; // OK: same as "C<T>* a;"
C<void>& b; // OK
X<C> c; // OK: C without a template argument list denotes the template C
X<::C> d; // OK: ::C is not the injected class name and therefore always
// denotes the template
};
```

Note how the unqualified name refers to the injected name and is not considered the name of the template if it is not followed by a list of template arguments. To compensate, we can force the name of the template to be found by using the file scope qualifier ::.

The injected class name for a variadic template has an additional wrinkle: If the injected class name were directly formed by using the variadic template’s template parameters as the template arguments, the injected class name would contain template parameter packs that have not been expanded (see Section 12.4.1 on page 201 for details of pack expansion). Therefore, when forming the injected class name for a variadic template, the template argument that corresponds to a template parameter pack is a pack expansion whose pattern is that template parameter pack: Click here to view code image

```
template<int I, typename... T> class V {
V* a; // OK: same as "V<I, T...> * a;"
V<0, void> b; // OK
};
```

## 13.2.4 Current Instantiations

The injected class name of a class or class template is effectively an alias for the type being defined. For a nontemplate class, this property is obvious, because the class itself is the only type with that name and in that scope. However, inside a class template or a nested class within a class template, each template instantiation produces a different type. This property is particularly interesting in that context, because it means that the injected class name refers to the same instantiation of the class template rather than some other specialization of that class template (the same holds for nested classes of class templates).

Within a class template, the injected class name or any type that is equivalent to the injected class name (including looking through type alias declarations) of any enclosing class or class template is said to refer to a current instantiation. Types that depend on a template parameter (i.e., dependent types) but do not refer to a current instantiation are said to refer to an unknown specialization, which may be instantiated from the same class template or some entirely different class template. The following example illustrates the difference: Click here to view code image

```
template<typename T> class Node {
using Type = T;
Node* next; // Node refers to a current instantiation
Node<Type>* previous; // Node<Type> refers to a current instantiation
Node<T*>* parent; // Node<T*> refers to an unknown specialization
};
```

Identifying whether a type refers to a current instantiation can be confusing in the presence of nested classes and class templates. The injected class names of *enclosing* classes and class templates (or types equivalent to them) do refer to a current instantiation, while the names of other nested classes or class templates do not: Click here to view code image

```
template<typename T> class C {
using Type = T;

struct I {
C* c; // C refers to a current instantiation
C<Type>* c2; // C<Type> refers to a current instantiation
I* i; // I refers to a current instantiation
};
struct J {
C* c; //C refers to a current instantiation
C<Type>* c2; // C<Type> refers to a current instantiation
I* i; // I refers to an unknown specialization,
// because I does not enclose
JJ* j; // J refers to a current instantiation
};
};
```

When a type refers to a current instantiation, the contents of that instantiated class are guaranteed to be instantiated from the class template or nested class thereof that is currently being defined. This has implications for name lookup when parsing templates—the subject of our next section—but it also leads to an alternative, more game-like way to determine whether a type X within the definition of a class template refers to a current instantiation or an unknown specialization: If another programmer can write an explicit specialization (described in detail in Chapter 16) such that X refers to that specialization, then X refers to an unknown specialization. For example, consider the instantiation of the type C<int>::J in the context of the above example: We know the definition of C<T>::J used to instantiate the concrete type (since that’s the type we’re instantiating). Moreover, because an explicit specialization cannot specialize a template or member of a template without also specializing all of the enclosing templates or members, C<int> will be instantiated from the enclosing class definition. Hence, the references to J and C<int> (where Type is int) within J refer to a current instantiation. On the other hand, one could write an explicit specialization for C<int>::I as follows: Click here to view code image

```
template<> struct C<int>::I {
// definition of the specialization
};
```

Here, the specialization of C<int>::I provides a completely different definition than the one that was visible from the definition of C<T>::J, so the I inside the definition of C<T>::J refers to an unknown specialization.

## 13.3 Parsing Templates

Two fundamental activities of compilers for most programming languages are tokenization—also called scanning or lexing—and parsing. The tokenization process reads the source code as a sequence of characters and generates a sequence of tokens from it. For example, on seeing the sequence of characters int* p = 0;, the “tokenizer” will generate token descriptions for a keyword int, a symbol/operator *, an identifier p, a symbol/operator =, an integer literal 0, and a symbol/operator ;.

A parser will then find known patterns in the token sequence by recursively reducing tokens or previously found patterns into higher level constructs. For example, the token 0 is a valid expression, the combination * followed by an identifier p is a valid declarator, and that declarator followed by “=” followed by the expression “0” is a valid init-declarator. Finally, the keyword int is a known type name, and, when followed by the init-declarator * p = 0, you get the initializing declaration of p.

### 13.3.1 Context Sensitivity in Nontemplates

As you may know or expect, tokenizing is easier than parsing. Fortunately, parsing is a subject for which a solid theory has been developed, and many useful languages are not hard to parse using this theory. However, the theory works best for context-free languages, and we have already noted that C++ is context sensitive. To handle this, a C++ compiler will couple a symbol table to the tokenizer and parser: When a declaration is parsed, it is entered in the symbol table. When the tokenizer finds an identifier, it looks it up and annotates the resulting token if it finds a type.

For example, if the C++ compiler sees
x*

the tokenizer looks up X. If it finds a type, the parser sees `identifier, type, X symbol, *` and concludes that a declaration has started. However, if X is not found to be a type, then the parser receives from the tokenizer `identifier, nontype, X symbol, *` and the construct can be parsed validly only as a multiplication. The details of these principles are dependent on the particular implementation strategy, but the gist should be there.

Another example of context sensitivity is illustrated in the following expression: `X<1>(0)`

If X is the name of a class template, then the previous expression casts the integer 0 to the type `X<1>` generated from that template. If X is not a template, then the previous expression is equivalent to `(X<1)>0`.

In other words, X is compared with 1, and the result of that comparison—true or false, implicitly converted to 1 or 0 in this case—is compared with 0. Although code like this is rarely used, it is valid C++ (and valid C, for that matter). A C++ parser will therefore look up names appearing before a `<` and treat the `<` as an angle bracket only if the name is known to be that of a template; otherwise, the `<` is treated as an ordinary less-than operator.

This form of context sensitivity is an unfortunate consequence of having chosen angle brackets to delimit template argument lists. Here is another such consequence: [Click here to view code image](#code-image)

```
template<bool B>
class Invert {
public:
static bool const result = !B;
};

void g()
{
bool test = Invert<(1>0)>::result; // parentheses required!
}
```

If the parentheses in `Invert<(1>0)>` were omitted, the greater-than symbol would be mistaken for the closing of the template argument list. This would make the code invalid because the compiler would read it to be equivalent to `((Invert<1>))0>::result`.⁴

The tokenizer isn’t spared problems with the angle-bracket notation either. For
