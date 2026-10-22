```
// sort a tuple based on comparing the element types:
template<template<typename T, typename U> class Compare,
typename... Elements>
auto sort(Tuple<Elements...> const& t)
{
return select(t,
InsertionSort<MakeIndexList<sizeof...(Elements)>,
MetafunOfNthElementT<
Tuple<Elements...>, 
Compare>::template Apply>());
}
```

Look carefully at the use of InsertionSort: The actual typelist to be sorted is a list of indices into the typelist, constructed with MakeIndexList<>. Therefore, the result of the insertion sort is a set of indices into the tuple, which is then provided to select(). However, because the InsertionSort is operating on indices, it expects its comparison operation to compare two indices. The principle is easier to understand when considering a sort of the indices of a std::vector, as in the following (non-metaprogramming) example: Click here to view code image

# tuples/indexsort.cpp

```
#include <vector>
#include <algorithm>
#include <string>

int main()
{
std::vector<std::string> strings = {"banana", "apple", "cherry"};
std::vector<unsigned> indices = { 0, 1, 2 };
std::sort(indices.begin(), indices.end(),
[&strings](unsigned i, unsigned j) {
return strings[i] < strings[j];
});
}
```

Here, indices contains indices into the vector strings. The sort() operation sorts the actual indices, so the lambda provided as the comparison operation accepts two unsigned values (rather than string values). However, the body of the lambda uses those unsigned values as indices into the strings vector, so the ordering is actually according to the contents of strings. At the end of the sort, indices provides indices into strings, sorted based on the values in strings.

Our use of InsertionSort for the tuple sort() employs the same