With this solution, we can produce a Tuple that applies the EBCO while maintaining initialization order and support for multiple elements of the same type: Click here to view code image

# tuples/tuplestorage3.hpp

```
template<typename... Types>
class Tuple;

// recursive case:
template<typename Head, typename... Tail>
class Tuple<Head, Tail...>
: private TupleElt<sizeof...(Tail), Head>, private Tuple<Tail...>
{
using HeadElt = TupleElt<sizeof...(Tail), Head>;
public:
Head& getHead() {
return static_cast<HeadElt *>(this)->get();
}
Head const& getHead() const {
return static_cast<HeadElt const*>(this)->get();
}
Tuple<Tail...>& getTail() { return *this; }
Tuple<Tail...> const& getTail() const { return *this; }
};

// basis case:
template<>
class Tuple<> {
// no storage required
};
```

With this implementation, the following program: Click here to view code image

# tuples/compressedtuple1.cpp

```
#include <algorithm>
#include "tupleelt1.hpp"
#include "tuplestorage3.hpp"
#include <iostream>

struct A {
A() {
std::cout << "A()" << '\n';
}
};

struct B {
B() {
std::cout << "B()" << '\n';
```