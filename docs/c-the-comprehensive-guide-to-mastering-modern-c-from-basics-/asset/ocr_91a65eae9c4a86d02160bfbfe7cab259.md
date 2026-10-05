```
| v::filter({const c::time_zone_link& l {
  return l.target()="Europe/Berlin";});
| v::transform({const c::time_zone_link& l)->string_view{
  return l.name());
},
 show,
 cout << "- Links to Europe/Berlin"; // Output: Arctic/Longyearbyen
}
```

**Listing 28.31** The time zone database.

# Standards and Implementations

The standard library defines the basis for the IANA time zone database should be used as the basis for implementations. However, this is not always easy because the database is not available on every system, and furthermore, is difficult to keep it up to date. Linux systems usually have the database installed (check in /usr/share/zoneinfo), but Windows systems do not. However, the Microsoft C++ compiler comes with the ICU library, contains a similar database. The differences are small but present.

# Compile-Time Fractions: "ratio"

In Table 28.6, you say that the second template parameter of duration is of ratio. Indeed, this ratio handles all the conversion that is so useful in <chrono>. What is useful for time units can be helpful elsewhere.

std::ratio is a fraction that is evaluated at compile-time. ratio<1,1000> is the compile-time equivalent of 1/1000. You can perform calculations with different ratio instances. The compiler even performs simplifications. This means that if you multiply ratio<100,1> by ratio<1,1000>, the result is not ratio<1000,100> by ratio<1,1>. This is important so that the compiler knows exactly when types are identical and when it needs to convert. If it is a "unit fraction," then you can omit the second template parameter because its default is 1. Thus, ratio<88> is the same as ratio<88,1>.

> "r Are Not Values, but Types!"

To emphasize once again: the ratio<1,2> a and ratio<1,3> b{} variables have different types. For example, if you write a void f(ratio<1,2> v) function, you cannot call it with f(ratio<1,3>{}). It makes little