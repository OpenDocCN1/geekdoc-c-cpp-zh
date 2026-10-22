```
```cpp
class Wrap {
  friend T;
  …
};
```
```

This is valid for any type T but is ignored if T is not actually a class type.

# 12.5.2 Friend Functions of Class Templates

An instance of a function template can be made a friend by making sure the name of the friend function is followed by angle brackets. The angle brackets can contain the template arguments, but if the arguments can be deduced, the angle brackets can be left empty: [Click here to view code image](#)

```
```cpp
template<typename T1, typename T2>
void combine(T1, T2);

class Mixer {
  friend void combine<>(int&, int&);
  // OK: T1 = int&, T2 = int&
  friend void combine<int, int>(int, int);
  // OK: T1 = int, T2 = int
  friend void combine<char>(char, int);
  // OK: T1 = char T2 = int
  friend void combine<char>(char&, int);
  // ERROR: doesn't match combine() template
  friend void combine<>(long, long) { … }
  // ERROR: definition not allowed!
};
```
```

Note that we cannot *define* a template instance (at most, we can define a specialization), and hence a friend declaration that names an instance cannot be a definition.

If the name is not followed by angle brackets, there are two possibilities: 1. If the name isn’t qualified (in other words, it doesn’t contain `::`), it never refers to a template instance. If no matching nontemplate function is visible at the point of the friend declaration, the friend declaration is the first declaration of that function. The declaration could also be a definition.

2. If the name is qualified (it contains `::`), the name must refer to a previously declared function or function template. A matching function is preferred over a matching function template. However, such a friend declaration cannot be a definition. An example may help clarify the various possibilities: [Click here to view code image](#)