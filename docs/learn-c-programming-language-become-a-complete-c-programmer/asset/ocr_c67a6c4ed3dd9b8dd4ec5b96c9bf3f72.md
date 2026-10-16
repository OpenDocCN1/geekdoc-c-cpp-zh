move iterator’s operator_*( ) simply returns an rvalue reference (§7.7.2) to the element pointed to: std::move(q). For example:

```
vector<string> read_strings(istream&); auto vs = read_strings(cin);
// get some strings
vector<string> vs2;
copy(vs,back_inser ter(vs2)); // copystr ingsfrom vs into vs2
vector<string> vs3; copy(vs2,make_move_iterator(back_inser ter(vs3))); // movestr ingsfrom vs2 into vs3 This assumes that a container version of std::copy() has been defined.
```

# 33.3 Range Access Functions

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
template<typename T, siz e_t N> // forbuilt-in arrays
auto begin(T (&array)[N]) -> T*;
template<typename T, siz e_t N>
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