# ISO/IEC 14882:2017(E)

```
--n;
while(n > 0) {
  typename iterator_traits<BidirectionalIterator>::value_type
  tmp = *first;
  *first++ = --last;
  last = tmp;
  n -= 2;
}
```

--- end example[]

# 27.4.2 Standard iterator tags [std.iterator.tags]

+   1 It is often desirable for a template specialization to find out what is the most specific category of its iterator, so that the function can select the most efficient algorithm at compile time. To facilitate this, the library introduces category tags which are used as compile time tags for algorithm selection. We use input_iterator_tag, output_iterator_tag, forward_iterator_tag, bidirectional_iterator_tag, random_access_iterator_tag. For every iterator type Iterator_traits<Iterator>::category is defined to be the most specific category tag that describes the iter' behavior.

```
namespace std {
  struct input_iterator_tag {};
  struct output_iterator_tag {};
  struct forward_iterator_tag : public input_iterator_tag {};
  struct bidirectional_iterator_tag : public forward_iterator_tag {};
  struct random_access_iterator_tag : public bidirectional_iterator_tag {};
}
```

+   2 Example: For a program-defined BinaryTreeIterator, it could be included into the bidirectional category by specializing the iterator_traits template:
template<class T> struct iterator_traits<BinaryTreeIterator<T>> {
  using iterator_category = bidirectional_iterator_tag;
  using difference_type = ptrdiff_t;
  using value_type = T;
  using pointer = T*;
  using reference = T&;
};

--- example[]

+   3 Example: If evolve(O) is well defined for bidirectional iterators, but can be implemented more efficiently for random access iterators, then the implementation is as follows:
template<class BidirectionalIterator>
inline void
evolve(BidirectionalIterator first, BidirectionalIterator last) {
  evolve(first, last);
  typename iterator_traits<BidirectionalIterator>::iterator_category();
}
ntemplate<class BidirectionalIterator>
void evolve(BidirectionalIterator first, BidirectionalIterator last,
  random_iterator_tag) {
  // more generic, less efficient algorithm

27.4.2

© ISO/IEC 2017 - All rights reserved

963