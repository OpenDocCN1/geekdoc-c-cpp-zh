# Overloading the Stream Insertion and
Stream Extraction Operators as `friends`

Lines 9–10 of **Fig. 10.10** declare the overloaded stream insertion operator and the overloaded stream extraction operator as `friends` of class `Array`. When the compiler sees an expression like `cout << arrayObject`, it invokes *non-member function* `operator<<` with the call

```
```
operator<<(cout, arrayObject)
```
```

When the compiler sees an expression like `cin >> arrayObject`, it invokes *non-member function* `operator>>` with the call

```
```
operator>>(cin, arrayObject)
```
```

Again, these stream insertion and stream extraction operator functions *cannot* be members of class `Array`, because the `Array` object is always mentioned on the *right* side of the stream insertion or stream extraction operator.