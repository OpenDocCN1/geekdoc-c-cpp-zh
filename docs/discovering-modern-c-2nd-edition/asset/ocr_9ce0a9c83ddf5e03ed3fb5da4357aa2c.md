them all:

```
vector<float, col_major, stack> w;
```

When all template parameters are set to default values, we can of course omit them all. However, for grammatical reasons not discussed here, the angle brackets still need to be written:

Click here to view code image

```
vector x; // Special meaning in C++17 (cf. §3.4.4), error
before
vector<> y; // Looks a bit strange but is correct
```

The template defaults can refer to preceding parameters:

Click here to view code image

```
template <typename T, typename U = T>
class pair;
```

This is a class for two values that might have different types. If not we can declare the type just once:

Click here to view code image

```
pair<int, float> p1; // Object with an int and float value
pair<int> p2; // Object with two int values
```

The default can even be an expression of preceding parameters as we will see in Chapter 5.

# 3.3.2 Designing Uniform Class and Function Interfaces

=> c++03/accumulate_example.cpp

When we write generic classes and functions, we can ask ourselves the chicken-and-egg question: What comes first? We have the choice to write function templates first and adapt our classes to them by realizing the corresponding methods. Alternatively, we can develop the interface of our classes first and implement generic functions against this interface.

The situation changes a little bit when our generic functions should be able to handle intrinsic types or classes from the standard library. These classes cannot be changed, and we should adapt our functions to their