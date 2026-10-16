
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

## 33.2.2 Insert Iterators

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
fill_n(back_inserter(vi),200,7); // add 200 7s to the end of vi
}
```

When writing to an element through an insert iterator, the iterator inserts its value rather than overwriting the element pointed to. So, a container grows by one element each time a value is written to it through an insert iterator. Inserters are as simple and efficient as they are useful.

move iterator’s operator_*( ) simply returns an rvalue reference (§7.7.2) to the element pointed to: std::move(q). For example:

```
vector<string> read_strings(istream&); auto vs = read_strings(cin);
// get some strings
vector<string> vs2;
copy(vs,back_inserter(vs2)); // copy strings from vs into vs2
vector<string> vs3; copy(vs2,make_move_iterator(back_inserter(vs3))); // move strings from vs2 into vs3 This assumes that a container version of std::copy() has been defined.
```

## 33.3 Range Access Functions

In <iterator>, the standard library provides a nonmember begin() and end() functions for containers: begin() and end() (§iso.24.6.5)

p=begin(c) p is an iterator for the first element of c; c is a built-in array or has c.begin()
p=end(c) p is an iterator for the one-past-the-end of c; c is a built-in array or has c.end()
These functions are very simple:

Section 33.3 Range Access Functions 965

```
template<typename C>
auto begin(C& c) -> decltype(c.begin());
template<typename C>
auto begin(const C& c) -> decltype(c.begin());
template<typename C>
auto end(C& c) -> decltype(c.end());
template<typename C>
auto end(const C& c) -> decltype(c.end());
```

```
template<typename T, size_t N> // for built-in arrays
auto begin(T (&array)[N]) -> T*;
template<typename T, size_t N>
auto end(T (&array)[N]) -> T*;
```

These functions are used by the range for-statement (§9.5.1) but can of course also be used directly by users. For example:

```
template<typename Cont>
void print(Cont& c)
{
for(auto p=begin(c); p!=end(c); ++p) cout << *p << '\n';
}
```

```
void f() {
vector<int> v {1,2,3,4,5}; print(v);
int a[] {1,2,3,4,5};
print(a);
}
```

Had I said c.begin() and c.end(), the call print(a) would have failed.
A user-defined container with member begin() and end() automatically gets nonmember versions when <iterator> is #included. To provide nonmember begin() and end() for a container, My_container, that doesn’t have them, I have to write something like:

```
template<typename T>
Iterator<My_container<T>> begin(My_container<T>& c)
{
return Iterator<My_container<T>>{&c[0]}; // iterator to first element }
template<typename T>
Iterator<My_container<T>> end(My_container<T>& c) {
return Iterator<My_container<T>>{&c[0]+c.size()}; // iterator to last element }
```

Here, I assume that passing the address of the first element is a way to create an iterator to the first element of My_container and that My_container has a size().

## 33.4 Function Objects

Many of the standard algorithms take function objects (or functions) as arguments to control the way they work. Common uses are comparison criteria, predicates (functions returning bool), and arithmetic operations. In <functional>, the standard library supplies a few common function objects:

# Predicates (§iso.20.8.5, §iso.20.8.6, §iso.20.8.7)

p=equal_to<T>(x,y) p(x,y) means x==y when x and y are of type T
p=not_equal_to<T>(x,y) p(x,y) means x!=y when x and y are of type T
p=greater<T>(x,y) p(x,y) means x>y when x and y are of type T
p=less<T>(x,y) p(x,y) means x<y when x and y are of type T
p=greater_equal<T>(x,y) p(x,y) means x>=y when x and y are of type T
p=less_equal<T>(x,y) p(x,y) means x<=y when x and y are of type T
p=logical_and<T>(x,y) p(x,y) means x&&y when x and y are of type T
p=logical_or<T>(x,y) p(x,y) means x||y when x and y are of type T
p=logical_not<T>(x) p(x) means !x when x is of type T
p=bit_and<T>(x,y) p(x,y) means x&y when x and y are of type T
p=bit_or<T>(x,y) p(x,y) means x|y when x and y are of type T
p=bit_xor<T>(x,y) p(x,y) means x^y when x and y are of type T

For example:

```
vector<int> v;
// ...
sort(v.begin(),v.end(),greater<int>{}); // sort vinto decreasing order
```

Such predicates are roughly equivalent to simple lambdas. For example:

```
vector<int> v;
// ...
sort(v.begin(),v.end(),[](int a, int b) { return a>b; }); // sort vinto decreasing order
```

Note that logical_and and logical_or always evaluate both their arguments (&& and || do

**Arithmetic Operations (siso.20.8.4)**

**f=plus<T>(x,y)** f(x,y) means x+y when x and y are of type **T**
**f=minus<T>(x,y)** f(x,y) means x−y when x and y are of type **T**
**f=multiples<T>(x,y)** f(x,y) means x*y when x and y are of type **T**
**f=divides<T>(x,y)** f(x,y) means x/y when x and y are of type **T**

**f=modulus<T>(x,y)** f(x,y) means x%y when x and y are of type **T**
**f=negate<T>(x)** f(x) means−x when x is of type **T**

## 33.5 Function Adaptors

A function adaptor takes a function as argument and returns a function object that can be used to invoke the original function.

**Adaptors (siso.20.8.9, Siso.20.8.10, Siso.20.8.8)**

**g=bind(f,args)** g(args2) is equivalent to **f(args3)** where **args3** is obtained by replacing placeholders in **args** with arguments from **args2** for the use of placeholders, such as **_1**, **_2**, and **_3**

**g=mem_fn(f)** g(p,args) means p->f(args) if p is a pointer and **p.mf(args)** if p is not; **args** is a (possibly empty) list of arguments

**g=not1(f)** g(x) means !f(x)

**g=not2(f)** g(x,y) means !f(x,y)

The **bind()** and **mem_fn()** adaptors do argument binding, also called *Currying* or *partial evaluation*. These binders, and their deprecated predecessors (such as **bind1st()**, **mem_fun()**, and **mem_fun_ref()**), were heavily used in the past, but most uses seem to be more easily expressed using lambdas (§11.4).

### 33.5.1 bind()

Given a function and a set of arguments, **bind()** produces a function object that can be called with “the remaining” arguments, if any, of the function. For example:

```
double cube(double);

auto cube2 = bind(cube,2);
```

A call **cube2()** will invoke **cube** with the argument **2**, that is, **cube(2)**. We don’t have to bind every argument of a function. For example:

```
using namespace placeholders;
void f(int,const string&);
auto g = bind(f,2,_1); // bind f()’s first argument to 2
f(2,“hello”);
g(“hello”); // also calls f(2,“hello”);
```

The curious **_1** argument to the binder is a placeholder telling **bind()** where arguments to the resulting function object should go. In this case, **g()**’s (first) argument is used as **f()**’s second argument. The placeholders are found in the (sub)namespace **std::placeholders** that is part of **<functional>**. The placeholder mechanism is very flexible. Consider:
