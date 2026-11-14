```
auto [LU, p] = lu(A);
```

Not only is this simpler and clearer, it is even more efficient. For such examples we observed that modern compilers are able to apply copy elision to the tuple components so that LU and p are neither copied nor moved.

The other heterogeneous class in C++ is pair. It already existed in C++03 and still does. pair is equivalent to a tuple with two arguments. Conversions from one to another exist so pair and two-argument tuple can be exchanged with each other and even mixed. The examples in this section could all be implemented with pair. Instead of get<0>(t) we could also write t.first (and t.second for get<1>(t)).

# C++17 4.4.3 variant

=> c++17/variant_example.cpp

variant is the modern version of a classic C++ feature called union that we omitted for good reasons. There are two kinds of unions: one is pretty dangerous and the other much more dangerous.

The purpose of variant is to have objects that can store values of different types. In our program we choose a set of types, for instance int, double, and string, and a variant object can store any value of those types:

Click here to view code image

```
using my_variant = variant<int, double, string>;
my_variant var;
```

```
var = 3;
var = 4.2;
var = "Text";
```

We can access the value with get and an (zero-based) index. In var above, the string has index 2:

```
string s = get<2>(var);
```

To not bother with the order of types, we can use the type instead of the index:

```
s = get<string>(var);
```