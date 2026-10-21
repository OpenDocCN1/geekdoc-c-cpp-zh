```
}
else {
    val *= 2;
}
};
...
std::visit(dblvar, var);
```

Here, for a std::string alternative, the call of the generic lambda instantiates its generic function call template to compute:

```
val = val + val;
```

while for other alternatives, such as int or double, the call of the lambda instantiates its generic function call template to compute:

```
val *= 2;
```

Note that care must be taken to check against the type of val. Here, we check whether the type is convertible to std::string. The check

```
if constexpr(std::is_same_v<decltype(val), std::string>) {
```

would not work because the type of val is declared as int&, std::string&, or long double&.

# Return Values in Visitors

Function calls in visitors may return values provided they have the same return type. For example:

```
using IntOrDouble = std::variant<int, double>;

std::vector<IntOrDouble> coll { 42, 7.7, 0, -0.7};

double sum{0};
for (const auto& elem : coll) {
    sum += std::visit([] (const auto& val) -> double {
        return val;
    },
    elem);
}
```

The code above will add the value of each alternative to sum. It would not compile without the explicit specification of the return type in the lambda, because then the return types would differ.

# Using Overloaded Lambdas as Visitors

By using an overloader for function objects and lambdas, you can also define a set of lambdas where the best match is used as a visitor.

Assume the overloader overload is defined as follows:

```
tmpi/overload.hpp
```