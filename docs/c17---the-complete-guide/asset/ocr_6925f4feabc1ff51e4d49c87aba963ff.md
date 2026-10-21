```
}; 

// all deduced:
C c1(22, 44.3, "hi"); // OK: T1 is int, T2 is double, T3 is const char*
C c2(22, 44.3); // OK: T1 is int, T2 and T3 are double
C c3("hi", "guy"); // OK: T1, T2, and T3 are const char*
```

```
// only some deduced:
C<string> c4("hi", "my"); // ERROR: only T1 explicitly defined
C<> c5(22, 44.3); // ERROR: neither T1 not T2 explicitly defined
C<> c6(22, 44.3, 42); // ERROR: neither T1 nor T2 explicitly defined
```

```
// all specified:
C<string,string,int> c7; // OK: T1,T2 are string, T3 is int
C<int,string> c8(52, "my"); // OK: T1 is int,T2 and T3 are strings
C<string,string> c9("a", "b", "c"); // OK: T1,T2,T3 are strings
```

Note that the third template parameter has a default value. For this reason, you do not have to explicitly specify the last type if the second type is specified.

If you are wondering why partial specialization is not supported, here is the example that caused this decision:

```
std::tuple<int> t(42, 43); // still ERROR
```

std::tuple is a variadic template, so you could specify an arbitrary number of arguments. In this case, therefore, it is not clear whether specifying only one type is an error or whether this is intentional. It looks questionable at least.

Unfortunately, the inability to partially specialize means that a common unfortunate coding requirement is not solved. We still cannot easily use a lambda to specify the sorting criterion of an associative container or the hash function of an unordered container:

```
std::set<Cust> coll([] (const Cust& x, const Cust& y) {
return x.getName() > y.getName();
});
```

We still have to specify the type of the lambda. For example:

```
auto sortcrit = [] (const Cust& x, const Cust& y) {
return x.getName() > y.getName();
};

std::set<Cust, decltype(sortcrit)> coll(sortcrit); // OK
```

Specifying only the type does not work because then the container tries to create a lambda of the given type, which is not allowed in C++17, because the default constructor can be called only by the compiler. With C++20, this will be possible, provided the lambda does not capture anything.