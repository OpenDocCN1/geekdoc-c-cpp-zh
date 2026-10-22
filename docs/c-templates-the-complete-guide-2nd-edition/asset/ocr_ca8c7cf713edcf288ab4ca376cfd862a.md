```
{ public:
Head& getHead() {
// potentially ambiguous
return static_cast<TupleElt<Head> *>(this)->get();
}
Head const& getHead() const {
// potentially ambiguous
return static_cast<TupleElt<Head> const*>(this)->get();
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

While this approach has solved the initialization-ordering problem, it has introduced a new (worse) problem: We can no longer extract elements from a tuple that has two elements of the same type, such as Tuple<int, int>, because the derived-to-base conversion from a tuple to TupleElt of that type (e.g., TupleElt<int>) will be ambiguous.

To break the ambiguity, we need to ensure that each TupleElt base class is unique within a given Tuple. One approach is to encode the “height” of this value within its tuple, that is, the length of the tail tuple. The last element in the tuple will be stored with height 0, the next-to-last-element will be stored with height 1, and so on:⁹

Click here to view code image

tuples/tupleelt1.hpp

```
template<unsigned Height, typename T>
class TupleElt {
T value;
public:
TupleElt() = default;

template<typename U>
TupleElt(U&& other) : value(std::forward<U>(other)) { }

T& get() { return value; }
T const& get() const { return value; }
};
```