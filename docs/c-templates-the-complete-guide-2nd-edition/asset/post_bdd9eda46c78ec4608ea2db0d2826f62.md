
## 12.4.3 Function Parameter Packs

A *function parameter pack* is a function parameter that matches zero or more function call arguments. Like a template parameter pack, a function parameter pack is introduced using an ellipsis (...) prior to (or in the place of) the function parameter name and, also like a template parameter pack, a function parameter pack must be expanded by a pack expansion whenever it is used. Template parameter packs and function parameter packs together are referred to as *parameter packs.*

Unlike template parameter packs, function parameter packs are always pack expansions, so their declared types must include at least one parameter pack. In the following example, we introduce a new Point constructor that copy-initializes each of the mixins from supplied constructor arguments:

```cpp
template<typename... Mixins>
class Point : public Mixins...
{
double x, y, z;
public:
//default constructor, visitor function, etc. elided
Point(Mixins... mixins) // mixins is a function parameter pack
: Mixins(mixins)... { } //initialize each base with the supplied mixin value
};
```

```cpp
struct Color { char red, green, blue; };
struct Label { std::string name; };
Point<Color, Label> p({0x7F, 0, 0x7F}, {"center"});
```

A function parameter pack for a function template may depend on template parameter packs declared in that template, which allows the function template to accept an arbitrary number of call arguments without losing type information:

```cpp
template<typename... Types>
void print(Types... values);
```

```cpp
int main()
{
std::string welcome("Welcome to ");
print(welcome, "C++", 2011, '\n'); //calls print<std::string, char const*, int, char>
}
```

When calling the function template print() with some number of arguments, the types of the arguments will be placed in the argument pack to be substituted for the template type parameter pack `Types`, while the actual argument values will be placed into an argument pack to be substituted for the function parameter pack `values`. The process by which the arguments are determined from the call is described in detail in Chapter 15. For now, it suffices to note that the *i*th type in `Types` is the type of the *i*th value in `values` and that both of these parameter packs are available within the body of the function template `print()`.

The actual implementation of `print()` uses recursive template instantiation, a template metaprogramming technique described in Section 8.1 on page 123 and Chapter 23.

There is a syntactic ambiguity between an unnamed function parameter pack appearing at the end of a parameter list and a C-style “vararg” parameter. For example:

```cpp
template<typename T> void c_style(int, T...);
template<typename... T> void pack(int, T...);
```

In the first case, the `T...` is treated as `T, ...`: an unnamed parameter of type T followed by a C-style vararg parameter. In the second case, the `T...` construct is treated as a function parameter pack because T is a valid expansion pattern. The disambiguation can be forced by adding a comma before the ellipsis (which ensures the ellipsis is treated as a C-style “vararg” parameter) or by following the `...` by an identifier, which makes it a named function parameter pack. Note that in generic lambdas, a trailing `...` will be treated as denoting a parameter pack if the type that immediately precedes it (with no intervening comma) contains auto.

## 12.4.4 Multiple and Nested Pack Expansions

The pattern of a pack expansion can be arbitrarily complex and may include multiple, distinct parameter packs. When instantiating a pack expansion containing multiple parameter packs, all of the parameter packs must have the same length. The resulting sequence of types or values will be formed element-wise by substituting the first argument of each parameter pack into the pattern, followed by the second argument of each parameter pack, and so on. For example, the following function copies all of its arguments before forwarding them on to the function object `f`:

```cpp
template<typename F, typename... Types>
void forwardCopy(F f, Types const&... values) {
  f(Types(values)...);
}
```

The call argument pack expansion names two parameter packs, `Types` and `values`. When instantiating this template, the element-wise expansion of the `Types` and `values` parameter packs produces a series of object constructions, which builds a copy of the *i*th value in `values` by casting it to the *i*th type in `Types`. Under the syntactic interpretation of pack expansions, a three-argument `forwardCopy` would look like this:

```cpp
template<typename F, typename T1, typename T2, typename T3>
void forwardCopy(F f, T1 const& v1, T2 const& v2, T3 const& v3) {
  f(T1(v1), T2(v2), T3(v3));
}
```

Pack expansions themselves may also be nested. In such cases, each occurrence of a parameter pack is “expanded” by its nearest enclosing pack expansion (and only that pack expansion). The following example illustrates a nested pack expansion involving three different parameter packs:

```cpp
template<typename... OuterTypes>
class Nested {
  template<typename... InnerTypes>
  void f(InnerTypes const&... innerValues) {
    g(OuterTypes(InnerTypes(innerValues)...)...);
  }
};
```

In the call to `g()`, the pack expansion with pattern `InnerTypes(innerValues)` is the innermost pack expansion, which expands both `InnerTypes` and `innerValues` and produces a sequence of function call arguments for the initialization of an object denoted by `OuterTypes`. The outer pack expansion’s pattern includes the inner pack expansion, producing a set of call arguments for the function `g()`, created from the initialization of each of the types in `OuterTypes` from the sequence of function call arguments produced by the inner expansion. Under the syntactic interpretation of this pack expansion, where `OuterTypes` has two arguments and both `InnerTypes` and `innerValues` have three arguments, the nesting becomes more apparent:

```cpp
template<typename O1, typename O2>
class Nested {
  template<typename I1, typename I2, typename I3>
  void f(I1 const& iv1, I2 const& iv2, I3 const& iv3) {
    g(O1(I1(iv1), I2(iv2), I3(iv3)),
      O2(I1(iv1), I2(iv2), I3(iv3)));
  }
};
```

Multiple and nested pack expansions are a powerful tool (e.g., see Section 26.2).

## 12.4.5 Zero-Length Pack Expansions

The syntactic interpretation of pack expansions can be a useful tool for understanding how an instantiation of a variadic template will behave with different numbers of arguments. However, the syntactic interpretation often fails in the presence of zero-length argument packs. To illustrate this, consider the `Point` class template from Section 12.4.2 on page 202, syntactically substituted with zero arguments:

```cpp
template<>
class Point : {
Point() : { }
};
```

The code as written above is ill-formed, since the template parameter list is now empty and the empty base class and base class initializer lists each have a stray colon character.

Pack expansions are actually semantic constructs, and the substitution of an argument pack of any size does not affect how the pack expansion (or its enclosing variadic template) is parsed. Rather, when a pack expansion expands to an empty list, the program behaves (semantically) as if the list were not present. The instantiation `Point<>` ends up having no base classes, and its default constructor has no base class initializers but is otherwise well-formed. This semantic rule holds even when the syntactic interpretation of zero-length pack expansion would be well-defined (but different) code. For example:

```cpp
template<typename T, typename... Types>
void g(Types... values) {
    T v(values...);
}
```

The variadic function template `g()` creates a value `v` that is direct-initialized from the sequence of values it is given. If that sequence of values is empty, the declaration of `v` looks, syntactically, like a function declaration `T v()`. However, since substitution into a pack expansion is semantic and cannot affect the kind of entity produced by parsing, `v` is initialized with zero arguments, that is, value-initialization.[^11]
