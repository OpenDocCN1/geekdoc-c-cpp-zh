The `=` operator says to capture all variables by copy. The `this` operator also captures the current object by copy. You use `*this` to capture the current object by reference, which means you can make changes to it. In C++ 20, you can now use `[=, this]` to make it clear that you are capturing both variables and the current object by copy, rather than by reference. You can also use `[&, this]`, which indicates that you are capturing all variables by reference but capturing the object by copy.

# ## Finding other changes

Sometimes, despite having the best understanding possible of lambda expressions, things just don’t work when you code them and it appears that they should. Often, you find subtle changes to the specification that tell you why something is no longer working. For example, you can see some of these changes in the paper “P1091R2 Extending structured bindings to be more like variable declarations” at http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1091r2.html.

# # Working in Unevaluated Contexts

An unevaluated expression is a full expression; it doesn’t require evaluation at runtime. For example, the `typeof`, `sizeof`, `noexcept`, and `decltype` operators aren’t evaluated. In addition, the C++ 20 requires-expressions (see https://en.cppreference.com/w/cpp/language/constraints) aren’t evaluated. An unevaluated context is one in which C++ is looking for an unevaluated expression of some type. C++ 20 allows the use of lambda expressions in unevaluated expressions, template arguments, alias declarations, and `typedef` declarations.

To see how an unevaluated context works, the `PriorityQueue` example, shown in Listing 3-1, demonstrates how to add a lambda expression comparator within a `decltype()` to automatically sort the priority queue.

**LISTING 3-1:** Defining a Priority Queue Comparator

```
```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {
```
```