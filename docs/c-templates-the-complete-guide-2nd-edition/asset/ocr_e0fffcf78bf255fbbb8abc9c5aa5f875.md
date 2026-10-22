```
std::unordered_set<Customer,MyCustomerHash> coll; there is no match for the call to
```

Click here to view code image

```
const main()::MyCustomerHash (const Customer&) in the instantiation of
```

Click here to view code image

```
 noexcept(declval<const _Hash&>()(declval<const _Key&>()))
```

(declval<const _Hash&>() is an expression of type main()::MyCustomerHash). A possible “near match” candidate is Click here to view code image

```
std::size_t main()::MyCustomerHash::operator()(const Customer&)
```

which is declared as

Click here to view code image

```
std::size_t operator() (const Customer& c) {
^~~~~~~
```

and the last note says something about the problem: Click here to view code image

```
passing ‘const main()::MyCustomerHash*’ as ‘this’ argument discards qualifiers
```

Can you see what the problem is? This implementation of the std::unordered_set class template requires that the function call operator for the hash object be a const member function (see also Section 11.1.1 on page 159). When that’s not the case, an error arises deep in the guts of the algorithm.

All other error messages cascade from the first and go away when a const qualifier is simply added to the hash function operator: Click here to view code image

```
std::size_t operator() (const Customer& c) const {
...
}
```

Clang 3.9 gives the slightly better hint at the end of the first error message that operator() of the hash functor is not marked const: Click here to view code image

```
...
errornovel2.cpp:28:47: note: in instantiation of template class
’std::unordered_set<Customer
```