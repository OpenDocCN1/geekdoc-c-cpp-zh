A reverse iterator is a perfectly ordinary iterator, so I could write the loop explicitly:

```
template<typename C, Val v>
auto find_last(C& c, Val v) -> decltype(c.begin()) {
for (auto p = c.rbegin(); p!=c.rend(); ++p) if (*p==v) return --p.base();
return c.end();
}
// viewsequence in reverse order
// use c.end() to indicate “not found”
```

The equivalent code searching backward using a (forward) iterator is:

```
template<typename C>
auto find_last(C& c, Val v) -> decltype(c.begin())
{
for (auto p = c.end(); p!=c.begin(); ) // search backward from end
if (*--p==v) return p;
return c.end(); // use c.end() to indicate “not found” }
```

As for the earlier definitions of find_last(), this version requires at least a bidirectional iterator. Section 33.2.2 Insert Iterators 963

# 33.2.2 Insert Iterators

Producing output through an iterator into a container implies that elements following the one pointed to by the iterator can be overwritten. This implies the possibility of overflow and consequent memory corruption. For example:

```
void f(vector<int>& vi)
{
fill_n(vi.begin(),200,7); // assign 7 to vi[0]..[199]
}
```

If vi has fewer than 200 elements, we are in trouble.

In <iterator>, the standard library provides a solution in the form of an inserter: when written to, an inserter inserts a new element into a sequence rather than overwriting an existing element. For example:

```
void g(vector<int>& vi)
{
fill_n(back_inser ter(vi),200,7); // add 200 7s to the end of vi
}
```

When writing to an element through an insert iterator, the iterator inserts its value rather than overwriting the element pointed to. So, a container grows by one element each time a value is written to it through an insert iterator. Inserters are as simple and efficient as they are useful.