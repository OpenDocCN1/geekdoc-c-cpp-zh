```
return tuple<matrix, vector>(LU, p);
}
```

Now we can immediately split up in our application the returned object into the (factorized) matrix and the (permutation) vector:

```
auto [LU, p] = lu(A);
```

The types of LU and p are deduced.

Structured bindings come in handy when we iterate over a map whose value_type is a pair of the key and its associated value. Instead of accessing the pair member with first and second, we can name them now key and value:

![](bbox=[0.133, 0.353, 0.383, 0.372])

```
map<string, int> numbers= {("Zero", 0), {"One", 1}, {"Two", 2}};
```

```
for (const auto& [key , value] : numbers)
cout << key << "->" << value << endl;
```

Here we accessed the key and value as a constant reference. Note that even without the const:

![](bbox=[0.133, 0.531, 0.383, 0.55])

```
for (auto& [key, value] : numbers)
cout << key << "->" << value << endl;
```

we couldn't change the key. The reason is that we split up an object of type pair<const string, int> (how the entries of the map are stored internally) and the type of the first reference is deduced to const string& in the same fashion as the constant argument in Section 3.1.2.2.

```
=> c++17/structured_bindings_user.cpp
```

This nice new feature is fortunately not limited to standard types but can be applied on user types as well. It is most easily used on aggregate types with public members only. Our lu result could be returned in a user class that merely bundles the two objects:

![](bbox=[0.133, 0.851, 0.383, 0.87])