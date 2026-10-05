The Increment functor is indeed a rather complicated representative of its kind. In fact, the typical functor has neither an internal state like amount_ nor modifiers like clear(). The typical functor is actually more like a different way to write a function—pardon me, a callable object.

Thus, function objects then integrate into the rest of the C++ structure:

+   - You can write class hierarchies with operator().
- operator() can be virtual.
- You can overload operator()—that is, write multiple variants with different parameter types.
- You can represent internal states, as you have seen, and create variants via constructors.
- And, but not least, you manipulate function objects like any other objects—for example, to put them in a container.

> Most functors are rather simple in design. You often use them as an interface between your own classes and the containers and algorithms of the standard library.

# 23.3.4 Practical Functors

A set<Type> is always sorted according to operator<Type, Type>. For example, you can create a list sorted by name with set<Dwarf> and the appropriate operator<.

```
// https://godbolt.org/z/3ch51ov87
#include <set>
```