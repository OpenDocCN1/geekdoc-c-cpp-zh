resulting value is p’s value before the decrement
p[n] Access (subscripting): p[n] refers to the element pointed to by p+n; equivalent to *(p+n)
p->n Access (member access): equivalent to (*p).m
p==q Equality: Do p and q point to the same element or do both point to the one-beyond-the-last element?
p!=q Inequality: !(p==q)
p<q Does p point to an element before the one q points to?
p<=q p<q || p==q
p>q Does p point to an element after the one q points to?
p>=q p>q || p==q
p+=n Advance n: make p point to the nth element after the one to which it points
p-=n Advance−n: make p point to the nth element before the one to which it points
q=p+n q points to the nth element after the one p points to
q=p−n q points to the nth element before the one p points to

A ++p returns a reference to p, whereas p++ must return a copy of p holding the old value. Thus, for more complicated iterators, ++p is likely to be more efficient than p++. The following operations work for every iterator for which they can be implemented, but they may work more efficiently for random-access iterators (see §33.1.2):

advance(p)
x=distance(p,q) q=next(p,n)

# Iterator Operations (§iso.24.4.4)

Like p+=n; p must be at least an input iterator Like x=q−p; p must be at least an input iterator Like q=p+n; p must be at least a forward iterator

q=next(p) q=next(p,1)
q=prev(p,n) Like q=p−n; p must be at least a bidirectional iterator q=prev(p)
q=prev(p,1)

In each case, if p is not a random-access iterator, the algorithm will take n steps.

# 33.2 Iterator Adaptors

In <iterator>, the standard library provides adaptors to generate useful related iterator types from a given iterator type:

reverse_iterator
back_insert_iterator front_insert_iterator insert_iterator
move_iterator
raw_storage_iterator

# Iterator Adaptors

+   Iterate backward §33.2.1
+   Insert at end §33.2.2
+   Insert at beginning §33.2.2
+   Insert anywhere §33.2.2