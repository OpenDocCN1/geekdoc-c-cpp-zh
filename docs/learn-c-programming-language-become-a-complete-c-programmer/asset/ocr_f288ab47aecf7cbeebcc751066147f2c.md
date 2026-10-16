p2 points to the first element in [b2:b2+(e−b)) such that !f(*p1,*p2) or p1==e

The mismatch() looks for the first pair of elements of two sequences that compare unequal and returns iterators to those elements. No end is specified for the second sequence; that is, there is no last2. Instead, it is assumed that there are at least as many elements in the second sequence as in the first, and first2+(last−first) is used as last2. This technique is used throughout the standard library, where pairs of sequences are used for operations on pairs of elements. We could implement mismatch() like this:

```
template<class In, class In2, class Pred = equal_to<Value_type<In>>>
pair<In, In2> mismatch(In first, In last, In2 first2, Pred p ={}) {
while ( first != last && p(*first,*first2)) {
++first;
++first2;
}
return {first,first2};
}
```

I used the standard function object equal_to (§33.4) and the type function Value_type (§28.2.1). Section 32.4.6 search() 935

# 32.4.6 search()

The search() and search_n() algorithms find one sequence as a subsequence in another:

```
p=search(b,e ,b2,e2)
p=search(b.e ,b2,e2,f)
p=search_n(b,e ,n,v)
```

# Searching for Sequences (§iso.25.2.13)

p points to the first *p in [b:e) such that [ p:p+(e−b)) equals [b2:e2) p points to the first *p in [b:e) such that [p:p+(e−b)) equals [b2:e2), using f for element comparison p points to the first element of [b:e) such that each element of [p:p+n) has the value v p=search_n(b,e ,n,v,f) p points to the first element of [b:e) such that for each element *q in [p:p+n) we have f(*p,v)

The search() algorithm looks for its second sequence as a subsequence of its first. If that second sequence is found, an iterator for the first matching element in the first sequence is returned. As usual, the end of the sequence is used to represent “not found.” For example:

```
string quote {“Why waste time learning, when ignorance is instantaneous?”};
```