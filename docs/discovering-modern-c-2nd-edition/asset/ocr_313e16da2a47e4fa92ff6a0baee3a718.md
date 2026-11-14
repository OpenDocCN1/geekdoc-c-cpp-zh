Back to our sum function, it computes the addition of the first entry with the sum of the others. This sum in turn is computed in the same manner recursively. To terminate the recursion, we write an overload for a single argument. We could have also written an overload for a nullary function (one without arguments) returning 0 as int.

Our implementation has a significant disadvantage: the return type is the type of the first argument—here int. This might work more or less in some cases:

Click here to view code image

```
auto s = sum(-7, 3.7f, 9u, -2.6);
std::cout << "s is " << s
          << " and its type is " << typeid(s).name() << ".\n";
```

This yields:

```
s is 2 and its type is int.
```

The correct result of 3.1 cannot be stored as int.18 This isn’t really satisfying but it can be much worse as in the following computation:

18. The output of typeid must be demangled on Linux with tools like c++filt. Visual Studio is so kind to provide true type names.

```
auto s2= sum(-7, 3.7f, 9u, -42.6);
```

This also returns an int:

```
s2 is -2147483648 and its type is int.
```

The first intermediate result is 9 - 42.6 = -33.6, which yields a very large number when converted to unsigned and is later turned into a very small int value. On the other hand, the calculation:

```
auto s = -7 + 3.7f + 9u + -42.6;
```

computes the correct result and stores it as double. But before we condemn variadic templates, we have to admit to ourselves that we chose inappropriate types for intermediate values and the final result. We will correct this in Section 5.2.7 with a better suited return type. Alternatively, a return type deduced with auto solves this problem as well.