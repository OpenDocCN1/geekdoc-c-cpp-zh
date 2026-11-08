
This term is somewhat misleading, because it is the name of a pre-defined C++ header. But the term "injected" names the official term because the name is injected into the including scope, making these visible to normal name lookup. In our example above, this would mean that both code fragments would be well-formed. This chapter therefore further details the history of fixed name injection.

### 13.2.2 Injected Class Names

The name of a class is injected inside the scope of that class itself and therefore accessible as an unqualified name in that scope. (However, it is not accessible as a qualified name because this is the rule used to declare the constructor. For example:

Click here to view code image

```cpp
template<typename T>
class C {
  private:
    T t[10];
  public:
    static int i[5];
};

template<typename T>
int C<T>::i[5] = {};

int main()
{
    std::cout << "C<T>::i = " << C<int>::i << '\n'
              << "C<T>::i = " << C<long>::i << '\n';
}
```

The member function C<T>::i returns the size of type C, whereas the function i returns the number of the variable (in other words, the size of an int object).

Class templates also have injected class names. However, they're stranger than ordinary injected class names: They can also be followed by template arguments (in which case they are injected class template names) but if they are not followed by template arguments they represent the class with its parameters as its arguments (or, for a partial specialization, its specialization arguments) if the context expects a type, or a template if the context expects a template. This explains the following situation:

Click here to view code image

```cpp
template<typename T> class X {
};

template<typename T> class X<T*> {
};

X x1;         // OK: see "class X" above
X<double> x2; // OK
X<int*> x3;   // OK: see "class X<T*>" above

template<typename T>
class C {
  ...
  C* c;       // OK: C is injected class name
              //    and therefore always
              //    denotes the template
};
```

Note how the injected name refers to the injected name and not a substituted name of the template if it is not followed by a list of template arguments. To compensate, you can force the name of the template to be followed by using the scope qualifier ::.

The injected class name for a variable template has an additional wrinkle: If the injected class name were directly formed by using the variable template's template parameters as the template arguments, the injected class name would contain template parameter packs (but we have seen that pack names would contain template parameter packs) but have no ... (we saw in Section 12.4.1 on page 405 for details of pack expansion). Therefore, when forming the injected class name for a variable template, the template arguments that correspond to a template parameter pack in a pack expansion where the pattern is a template parameter pack.

Click here to view code image

### 13.2.4 Current Instantiations

The injected class name of a class or class template is effectively an alias for the type being defined. For a non-template class, this property is obvious, because the class itself is the only type with that name and in that scope. However, inside a class template a named class within a class template, each template instantiation produces a different type. This property is particularly interesting in that context, because it means that the injected class name refers to the same instantiation of the class template rather than some other specialization of that class template (that which holds for related classes of class templates).

Within a class template, the injected class name can use type that is equivalent to the injected class name (including looking through type aliases) but it always refers to an instantiation of that class (or class template) not a prior specialization. Thus, the class declared as a template parameter (e.g., a dependent type) does not refer to a current instantiation and is said to refer to an unknown specialization, which may be instantiated from the same class template or some entirely different class template. The following example illustrates the difference:

**Click here to view code image**

```cpp
template<typename T> class Node {
    using Type = T;
    Node* next;          // No reference to a current instantiation
    Node<Type>* previous; // Node<Type> refers to a current instantiation
    Node<T>* parent;      // Node<T> refers to an unknown instantiation
};
```

Identifying whether a type refers to a current instantiation can be confusing in the presence of nested classes and class templates. The injected class name of an enclosing class and class template does not refer to a current instantiation, while the name of other nested classes or class templates does not refer to a current instantiation.

**Click here to view code image**

```cpp
template<typename T> class C {
    using TType = T;

    struct D {
        C<T>* c;          // C<T> refers to a current instantiation
        C<TType>* c2;      // C<TType> refers to a current instantiation
        T* i;              // T refers to a current instantiation

        struct J {
            C<T>* c;       // C<T> refers to a current instantiation
            C<TType>* c2;   // C<TType> refers to a current instantiation
            T* j;           // T refers to an unknown specialization,
                           // because J does not enclose
                           // the type T
        };
    };
};
```

When a type refers to a current instantiation, the contents of that instantiated class are guaranteed to be instantiated from the class template or nested class thereof that is currently being defined. This has implications for name lookup when parsing templates—the subject of our next section—but it also leads to an alternative, more game-like way to determine whether a type within the definition of a class template refers to a current instantiation. If another programmer can write an explicit specialization such that it refers to that specialization, then it refers to an unknown specialization. For example, consider the instantiation of the type C<int> in the context of the above example: We know the definition of C<int> need not instantiate the concrete type (since that's the type we're instantiating). However, because an explicit specialization of a member of a template without also specializing all of the enclosing templates or members, C<int> will be instantiated from the enclosing class definition. Hence, the reference to D and C<T> (where T is int) within C<int> refers to a current instantiation.

**Click here to view code image**

```cpp
template<> struct C<int> {
    // definition of C<int>
};
```

Here, the specialization of C<int> provides a completely different definition than the one that was visible from the definition of C<T>; so in the inside definition of C<T>::... refers to an unknown specialization.

## 13.3 PARSING TEMPLATES

Two fundamental activities of compilers for most programming languages are resolution—also called name lookup or lexing—and parsing. The tokenization process reads the source code as a sequence of characters and generates a sequence of tokens from it. For example, on seeing the sequence of characters "int * p;", the "tokenizer" will generate ten descriptions for a keyword, an identifier, an operator, and an identifier. Parsing reduces tokens of previously found patterns into higher-level constructs. For example, the token `is` is a valid expression, the combination `+` followed by an identifier is a valid decorator, and that decorator followed by `~` followed by the expression `0` is a valid if-decorator. Finally, the keyword `int` is a known type name, and when followed by the initializer-declarator `= p`, you get the initializing declaration of `p`.

### 13.3.1 Context Sensitivity in Nontemplates

As you may know or expect, tokenizing is easier than parsing. Fortunately, parsing is a subject for which a solid theory has been developed, and many useful languages are not hard to parse using this theory. However, the theory works best for context-free languages, and we have already pointed out that C++ is context sensitive. To handle this, a C++ compiler will couple a symbol table to the tokenizer and parser. When a declaration is parsed, it is entered in the symbol table. When the tokenizer finds an identifier, it looks it up and annotates the resulting token if it finds a type.

For example, if the C++ statement was

```
x* y;
```

the tokenizer looks up `x`. If it finds a type, the parser sees

```
identifier, type, x
symbol, *
```

and concludes that a declaration has started. However, if `x` is not found to be a type, then the parser receives from the tokenizer

```
identifier, nontype, x
symbol, *
```

and the construct can be parsed validly only as a multiplication. The details of these principles are dependent on the particular implementation strategy, but the gist should be there.

Another example of context sensitivity is illustrated in the following expression:

```
x[i]>(i)
```

If `x` is the name of a class template, then the previous expression casts the integer `i` to the type `x<i>` generated from that template. If `x` is not a template, then the previous expression is equivalent to

```
x[i] > (i)
```

In other words, `x` is compared with `i`, and the result of that comparison—true or false—is implicitly converted to `1` or `0` in this case. Although code like this is rarely used, it is valid C++ (and valid C, for that matter). A C++ parser will therefore look up names appearing before an `<`, and treat them as a type—and hence treat `<` and `>` as angle brackets—only if the name is known to be that of a template; otherwise, the `<` is treated as an ordinary less-than operator.

This form of context sensitivity is an unfortunate consequence of having chosen angle brackets to delimit template argument lists. Here is another such consequence:

Click here to view code image

```cpp
template<class T>
class Vector {
public:
  static bool const result = T>0;
};

void g() {
  bool test = Vector<1>(0)>result;  // parentheses
}
```

If the parentheses in `Vector<1>(0)>` were omitted, the greater-than symbol would be mistaken for the closing of the template argument list. This would make the code invalid because the compiler would read it to be equivalent to `Vector<1>(0) > result`.

The tokenizer isn't spared problems with the angle-bracket notation either. For example, in

Click here to view code image

```cpp
List<List<int>> x;    // no space between right angle brackets
```

the two `>` characters combine into a right-shift token `>>` and hence are never treated as two separate tokens by the tokenizer. This is a consequence of the maximum munch tokenization principle: A C++ implementation must collect as many consecutive characters as possible into a token.

As mentioned in Section 2.2 on page 28, since C++11, the C++ standard specifically calls out this case—where a nested template-id is closed by a right-shift token (`>>`)—and hence the parser treats this right-shift token as two separate right angle brackets (`> >`). It's interesting to note that this change subtly changed the meaning of some—admittedly contrived—programs. Consider the following example:

Click here to view code image

```cpp
#include <iostream>
```
