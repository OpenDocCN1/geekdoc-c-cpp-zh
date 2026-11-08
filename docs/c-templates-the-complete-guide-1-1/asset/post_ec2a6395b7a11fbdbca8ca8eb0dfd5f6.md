
initialized from the sequence of values it is given. If that sequence of values is empty, the declaration of `values` is syntactically like a function declaration. However, since substitution into a pack expression is recursive and cannot affect the kind of entity produced by parsing, `v` is initialized with zero arguments, that is, value-initialization.

### 12.4.6 Fold Expressions

A recurring pattern in programs is the fold of an operation on a sequence of values. For example, a right fold of a function `f` over a sequence of values `x₁, x₂, ..., xₙ` is:

`f(x₁, f(x₂, ..., f(xₙ₋₁, xₙ)...))`

In general, a fold is a way of combining all the arguments of a function using a single operation. The C++ committee ran into the need to deal with such constructs for the special case of a logical binary operator (i.e., `&&` or `||`) applied to a pack expansion. Without an extra feature, we might write the following code to achieve that for the `&&` operator:

```cpp
bool and_all() { return true; }

template<typename ... Ts>
bool and_all(Ts ... ts)
{
    bool result = true;
    for (bool b : {ts...})
        result = result && b;
    return result;
}
```

With C++17, a new feature called fold expressions was added (see Section 6.2 on page 96 for an introduction). It applies to all binary operators except `.` and `?:`, and provides:

Given an expanded expression pattern `pack` and a non-pack expression value, C++17 allows us to write for any such operator `op`, either

`(pack op ... op value)`

for a right fold of the operator (called a binary right fold), or

`(value op ... op pack)`

for a left fold (called a binary left fold).

With this feature available, code like

```cpp
template<typename ... Ts>
auto sum(Ts ... ts)
{
    return (ts + ...);
}
```

can be written. The `and_all` function defined above can instead be written as

```cpp
template<typename ... Ts>
bool and_all(Ts ... ts)
{
    return (ts && ...);
}
```

As you’d expect, fold expressions are pack expansions. Note that if the pack is empty, the type of the fold expression can still be determined from the non-pack operand (value in the forms above).

However, the designers of this feature also wanted an option to leave out the value operand. Two other forms are therefore available in C++17:

The unary right fold `(pack op ...)` and the unary left fold `(... op pack)`. Again, the parentheses are required. Clearly this creates a problem for empty expansions: How do we determine their type and value? The answer is that an empty expansion of a unary fold is generally an error, with three exceptions:

- An empty expansion of a unary fold of `&&` produces the value `true`.
- An empty expansion of a unary fold of `||` produces the value `false`.
- An empty expansion of a unary fold of `,` produces the `void()` expression.

Notice that this will create surprises if you overload one of these special operators in a somewhat unusual way. For example:

```cpp
struct BooleanSymbol
{
};

BooleanSymbol operator||(BooleanSymbol, BooleanSymbol);

template<typename ... Ts>
BooleanSymbol all(BooleanSymbol ... symbols)
{
    BooleanSymbol result = {};
    ...
}
```

## 12.5 Friends

The basic idea of friend declaration is a simple one: identify classes or functions that have a privileged connection with the class in which the friend declaration appears. Matters are somewhat complicated, however, by two facts:

- 1. A friend declaration may be the only declaration of an entity.
- 2. A friend function declaration can be a definition.

### 12.5.1 Friend Classes of Class Templates

Friend class declarations cannot be definitions and therefore are rarely problematic. In the context of templates, the only new facet of friend class declarations is the ability to name a particular instance of a class template as a friend:

```cpp
template<typename T>
class Node
{
    ...
};

template<typename T>
class Tree
{
    friend class Node<T>;
};
```

Note that the class template must be visible at the point where one of its instances is made a friend of a class or class template. With an ordinary class, there is no such requirement:

**Click here to view code image**

```cpp
template<typename T>
class Tree
{
    friend class Fallback;  // OK even if first declaration
    ...
    friend class Node<T>;   // error if Node isn't visible
};
```

Section 12.3.2 on page 230 has more to say about this.

One application introduced in Section 5.5 on page 75 is the declaration of other class template instantiations as friends:

**Click here to view code image**

```cpp
template<typename T>
class Stack
{
public:
    // assign stack of elements of type T
    template<typename U>
    Stack<T>& operator= (Stack<U> const&);
    // to get access to private members of Stack<T> for
    // any type T? 
    template<typename U> friend class Stack;
};
```

C++11 also added syntax to make a template parameter a friend:

```cpp
template<typename T>
class Node
{
    friend T;
};
```

This is valid for any type T but is ignored if T is not actually a class type.

### 12.5.2 Friend Functions of Class Templates

An instance of a function template can be made a friend by making sure the name of the friend function is followed by angle brackets. The angle brackets can contain the template arguments, but if the arguments can be deduced, the angle brackets can be left empty:

**Click here to view code image**

```cpp
template<typename T> void print(T);

class MyClass
{
    friend void print<>(MyClass const&);
};
```

Note that we cannot define a template instance (at most, we can define a specialization), and hence a friend declaration that names an instance cannot be a definition.

If the name is not followed by angle brackets, there are two possibilities:

- 1. If the name isn't qualified (in other words, it doesn't contain `::`), it refers to a template instantiation. In such a situation, the function must be visible at the point of the friend declaration, or the friend declaration is the first declaration of that function. The declaration could also be a definition.
- 2. If the name is qualified (it contains `::`), the name must refer to a pre-existing function or function template specialization, but not a function template.

Click here to view code image

```cpp
void multiply();                 // ordinary function

template<typename T>
void multiply(T);                 // function template

class Creator {
    friend void multiply() {     // defines a non-template function
        ...
    }

    friend void multiply(int);  // refers to the ordinary function above,
                                // not to the multiply<T> template

    template<typename T>
    friend void multiply(T) {   // refers to an instance of the template
        ...
    }
};
```

In our previous example, we declared the friend functions in an ordinary class. The same rules apply when we declare them in class templates, but the template parameters may participate in identifying the function that is to be a friend:

Click here to view code image

```cpp
template<typename T>
class Node {
    Node<T>* allocate();
};

template<typename T>
class List {
    friend Node<T>* Node<T>::allocate();
};
```

A friend function may also be defined within a class template, in which case it is only instantiated when it is actually used. This typically requires the friend function to use the class template itself in the type of the friend function, which makes it easier to express functions on the class template that can be called as if they were visible in namespace scope:

Click here to view code image

```cpp
template<typename T>
class Creator {
    friend void f(Creator<T>) {  // every T instantiates
                                  // a different function for each T
    }
};

int main()
{
    Creator<void> one;
    f(one);                      // instantiates
    Creator<Creator<void>> two;
    f(two);
    Creator<double> three;
    f(three);
}
```

In this example, every instantiation of Creator generates a different function. Note that even though these functions are generated as part of the instantiation of a template, the functions themselves are ordinary functions, not instances of a function template. However, they are considered instantiated entities (see Section 12.1 on page 181) and their definition is instantiated only when used. Note that because the function is defined inside a class definition, it is implicitly inline. Hence, it is not an error for the same function to be generated in two different translation units. Section 3.2.2 on page 99 and Section 12.1.1 on page 497 have more to say about this topic.

### 12.5.3 Friend Templates

Usually when declaring a friend that is an instance of a function or a class template, we can express exactly which entity is to be the friend. Sometimes it is nonetheless useful to express that all instances of a template are friends. This requires a friend template. For example:

Click here to view code image

```cpp
template<typename T>
class Task {
    template<typename T>
    friend class Task;

    template<typename T>
    ...
```
