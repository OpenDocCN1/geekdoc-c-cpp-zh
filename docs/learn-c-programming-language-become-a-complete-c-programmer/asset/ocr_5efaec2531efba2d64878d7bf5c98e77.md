Move rather than copy §33.2.3
Write to uninitialized storage §34.6.2.

Iterators for **iostreams** are described in §38.5.

# 33.2.1 Reverse Iterator

Using an iterator we can traverse a sequence `[b:e)` from **b** to **e**. If the sequence allows bidirectional access, we can also traverse the sequence in reverse order, from **e** to **b**. An iterator that does that is called a **reverse_iterator**. A **reverse_iterator** iterates from the end of the sequence defined by its underlying iterator to the beginning of that sequence. To get a half-open sequence, we must consider **b−1** as one past the end and **e−1** as the start of the sequence: `[e−1,b−1)`. Thus, the fundamental relation between a reverse iterator and its corresponding iterator is `&*_(reverse_iterator(p)) == &*_(p−1)`. In particular, if **v** is a **vector**, `v.rbegin()` points to its last element, `v[v.size()−1]`. Consider:

**begin() end()**
A B C

This sequence can be viewed like this using a **reverse_iterator**:

**rbegin() rend()**
C B A

The definition of **reverse_iterator** looks something like this:

```
template<typename Iter>
class reverse_iterator

: public iterator<Iterator_category<Iter>,
Value_type<Iter>,
Difference_type<Iter>,
Pointer<Iter>,
Reference<Iter>> {

public:
using iterator_type = Iter;

reverse_iterator(): current{} { }
explicit reverse_iterator(Iter p): current{p} { }
template<typename Iter2>
reverse_iterator(const reverse_iterator<Iter2>& p): current(p.base()) { }
Iter base() const { return current; } // current iterator value

reference operator *() const { tmp = current; return *--tmp; } pointer operator ->() const;
reference operator[](difference_type n) const;

reverse_iterator& operator++() { --current; return *this; } // note: not ++
reverse_iterator operator++(int) { reverse_iterator t = current; --current; return t; }
reverse_iterator& operator--() { ++current; return *this; } // note: not --
reverse_iterator operator--(int) { reverse_iterator t = current; ++current; return t; }
```