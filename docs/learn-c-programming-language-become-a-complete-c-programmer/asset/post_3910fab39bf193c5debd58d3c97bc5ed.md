
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

## 32.4.6 search()

The search() and search_n() algorithms find one sequence as a subsequence in another:

```
p=search(b,e ,b2,e2)
p=search(b.e ,b2,e2,f)
p=search_n(b,e ,n,v)
```

### Searching for Sequences (§iso.25.2.13)

p points to the first *p in [b:e) such that [ p:p+(e−b)) equals [b2:e2) p points to the first *p in [b:e) such that [p:p+(e−b)) equals [b2:e2), using f for element comparison p points to the first element of [b:e) such that each element of [p:p+n) has the value v p=search_n(b,e ,n,v,f) p points to the first element of [b:e) such that for each element *q in [p:p+n) we have f(*p,v)

The search() algorithm looks for its second sequence as a subsequence of its first. If that second sequence is found, an iterator for the first matching element in the first sequence is returned. As usual, the end of the sequence is used to represent “not found.” For example:

```
string quote {“Why waste time learning, when ignorance is instantaneous?”};
```

```
bool in_quote(const string& s) {
auto p = search(quote.begin(),quote.end(),s.begin(),s.end()); // find s in quote return
p!=quote.end();
}
```

```
void g() {
bool b1 = in_quote("learning"); // b1 = true
bool b2 = in_quote("lemming"); // b2 = false
}
```

Thus, search() is a useful algorithm for finding a substring generalized to all sequences. Use find() or binary_search() (§32.6) to look for just a single element.

## 32.5 Modifying Sequence Algorithms

The modifying algorithms (also called mutating sequence algorithms) can (and often do) modify elements of their argument sequences.

transform (§iso.25.3.4)

p=transform(b,e ,out,f) Apply *q=f(*p1) to every *p1 in [b:e), writing to the corresponding *q in [out:out+(e-b)); p=out+(e-b)

p=transform(b,e ,b2,out,f) Apply *q=f(*p1,*p2) to every element in *p1 in [b:e) and the corresponding *p2 in [b2:b2+(e-b)), writing to the corresponding *q in [out:out+(e-b)); p=out+(e-b) Somewhat confusingly, transform() doesn’t necessarily change its input. Instead, it produces an output that is a transformation of its input based on a user-supplied operation. The one-input-sequence version of transform() may be defined like this:

```
template<class In, class Out, class Op>
Out transform(In first, In last, Out res, Op op)
{
while ( first!=last)
*res++ = op(*first++);
return res;
}
```

The output sequence may be the same as the input sequence:

```
void toupper(string& s) // removecase
{
transform(s.begin(),s.end(),s.begin(),toupper);
}
```

This really transforms the input s.

### 32.5.1 copy()

The copy() family of algorithms copy elements from one sequence into another. The following sections list versions of copy() combined with other algorithms, such as

# replace_copy() (§32.5.3). The copy Family (§iso.25.3.1)

```
p=copy(b,e ,out)
p=copy_if(b,e ,out,f)
p=copy_n(b,n,out)
p=copy_backward(b,e ,out)
```

Copy all elements in [ b:e)to[out:p); p=out+(e−b) Copy elements x in [b:e) for which f(x) to [out:p) Copy the first n elements in [b:b+n)to[out:p); p=out+n Copy all elements in [b:e)to[out:p), starting with its last element; p=out+(e−b)

```
p=move(b,e ,out)
p=move_backward(b,e ,out)
```

Move all elements in [ b:e)to[out:p); p=out+(e−b) Move all elements in [b:e)to[out:p), starting with its last element; p=out+(e−b)

The target of a copy algorithm need not be a container. Anything that can be described by an output iterator (§38.5) will do. For example:

```
void f(list<Club>& lc, ostream& os)
{
copy(lc.begin(),lc.end(),ostream_iterator<Club>(os));
}
```

To read a sequence, we need a pair of iterators describing where to begin and where to end. To write, we need only an iterator describing where to write to. However, we must take care not to write beyond the end of the target. One way to ensure that we don’t do this is to use an inserter (§33.2.2) to grow the target as needed. For example:

# Section 32.5.1 copy() 937

```
void f(const vector<char>& vs, vector<char>& v) {
copy(vs.begin(),vs.end(),v.begin()); // might overwrite end of v
copy(vs.begin(),vs.end(),back_inserter(v)); // add elements from vs to end of v
}
```

The input sequence and the output sequence may overlap. We use copy() when the sequences do not overlap or if the end of the output sequence is in the input sequence. We use copy_if() to copy only elements that fulfill some criterion. For example:

```
void f(list<int>&ld, int n, ostream& os)
{
copy_if(ld.begin(),ld.end(), ostream_iterator<int>(os), [](int x) { return x>n; });
}
```

See also remove_copy_if().

### 32.5.2 unique()

The **unique()** algorithm removes adjacent duplicate elements from a sequence: **The unique Family (§iso.25.3.9)**

- **p=unique(b,e)** Move elements in [b:e) such that [b:p) has no adjacent duplicates
- **p=unique(b,e,f)** Move elements in [b:e) such that [b:p) has no adjacent duplicates; **f(*p,* (p+1))** defines “duplicate”
- **p=unique_copy(b,e,out)** Copy [b:e) to [out:p); don’t copy adjacent duplicates
- **p=unique_copy(b,e,f,out)** Copy [b:e) to [out:p); don’t copy adjacent duplicates; **f(*p,* (p+1))** defines “duplicate”

The **unique()** and **unique_copy()** algorithms eliminate adjacent duplicate values. For example:

```
void f(list<string>& ls, vector<string>& vs)
{
  ls.sort(); // list sort (§31.4.2)
  unique_copy(ls.begin(),ls.end(),back_inserter(vs));
}
```

This copies **ls** to **vs**, eliminating duplicates in the process. I used **sort()** to get equal strings adjacent. Like other standard algorithms, **unique()** operates on iterators. It does not know which container these iterators point into, so it cannot modify that container. It can only modify the values of the elements. This implies that **unique()** does not eliminate duplicates from its input sequence in the way we naively might expect. Therefore, this does not eliminate duplicates in a **vector**:

```
void bad(vector<string>& vs) // warning: doesn’t do what it appears to do!
{
  sort(vs.begin(),vs.end()); // sort vector
  unique(vs.begin(),vs.end()); // eliminate duplicates (no it doesn’t!)
}
```

Rather, **unique()** moves unique elements toward the front (head) of a sequence and returns an iterator to the end of the subsequence of unique elements. For example:

```
int main()
{
  string s = “abbcccde”;
  auto p = unique(s.begin(),s.end());
  cout << s << ‘ ‘ << p-s.begin() << ‘\n’;
}
```

produces

**abccde 5**

That is, **p** points to the second c (that is, the first of the duplicates).

Algorithms that might have removed elements (but can’t) generally come in two forms: the “plain” version that reorders elements in a way similar to **unique()** and a **_copy** version that produces a new sequence in a way similar to **unique_copy()**.

To eliminate duplicates from a container, we must explicitly shrink it:

```
template<class C>
void eliminate_duplicates(C& c)
{
sort(c.begin(),c.end()); // sort
auto p = unique(c.begin(),c.end()); // compact
c.erase(p,c.end()); // shrink
}
```

I could equivalently have written c.erase(unique(c.begin(),c.end()),c.end()), but I don’t think such terseness improves readability or maintainability.

### 32.5.3 remove() and replace()

The remove() algorithm “removes” elements to the end of a sequence:

```
p=remove(b,e ,v)
p=remove_if(b,e ,v,f)
p=remove_copy(b,e ,out,v) p=remove_copy_if(b,e ,out,f) reverse(b,e)
p=reverse_copy(b,e ,out) remove (§iso.25.3.8)
```

Remove elements with value v from [b:e), such that [b:p) becomes the elements for which !(*q==v) Remove elements *q from [b:e), such that [b:p) becomes the elements for which !f(*q) Copy elements from [b:e) for which !(*q==v) to [out:p) Copy elements from [b:e) for which !f(*q) to [out:p) Reverse the order of elements in [b:e) Copy [b:e) into [out:p) in reverse order

The replace() algorithm assigns new values to selected elements:

Section 32.5.3 remove() and replace() 939

```
replace(b,e,v,v2)
replace_if(b,e,f,v2)
p=replace_copy(b,e ,out,v,v2)
p=replace_copy_if(b,e ,out,f,v2) replace (§iso.25.3.5)
```

Replace elements *p in [b:e) for which *p==v with v2 Replace elements *p in [b:e) for which f(*p) with v2 Copy [b:e)to[out:p), replacing elements for which *p==v with v2 Copy [b:e)to[out:p), replacing elements for which f(*p,v) with v2

These algorithms cannot change the size of their input sequence, so even remove() leaves the size of its input sequence unchanged. Like unique(), it “removes” by moving elements to the left. For example:

```
string s {" *CamelCase*IsUgly*"};
cout << s << '\n'; // *CamelCase*IsUgly*
auto p = remove(s.begin(),s.end(),'*');
```
