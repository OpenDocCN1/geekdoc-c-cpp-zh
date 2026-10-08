We did a similar thing for PrintFunctor in the C++98/03 Chapter. In that class, we added a member variable std::string strText which was initialised in the constructor. Having a member variable allows us to store state in the callable object.

The syntax for captures:

+   - [&] capture by reference all automatic storage duration variables declared in the scope.
- [=] capture by value (create a copy) all automatic storage duration variables declared in the scope.
- [x, &] capture by value and y by a reference explicitly.
- [args...] - capture a template argument pack, all by value.
- [&args...] - capture a template argument pack, all by reference.

And a summary with examples:

```
int x = 2, y = 3;
const auto l1 = [&](){ return 1; }; // No capture
const auto l12 = [=](){ return x; }; // All by value (copy)
const auto l13 = [&](){ return y; }; // All by ref
const auto l14 = [x](){ return x; }; // Only x by value (copy)
// const auto l15 = [=](){ return x; }; // wrong syntax, no need for

const auto l15 = [&y](){ return y; }; // = to copy x explicitly
const auto l16 = [x, y](){ return x * y; }; // x by value and y by ref
const auto l17 = [, &x](){ return x + y; }; // All by value except x
const auto l18 = [&, y](){ return x - y; }; // which is ref
// // All by ref except which
// is by value
```

To understand what happens with a captured let's consider the following code sample:

# Capturing a Variable

```
std::string str("Hello World");
auto foo = [str]() { return std::cout << str << '\n'; };
foo();
```

For the lambda, str is captured by value (i.e. it is copied). The compiler will generate the local functor:

# A Possible Compiler Generated Functor, Single Variable

```
struct _unnamedLambda {
_unnamedLambda(std::string s) : str(s) {} // copy
```

![](bbox=[0.415, 0.936, 0.585, 0.955])