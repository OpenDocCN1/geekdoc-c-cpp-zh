```
functions.push_back(mult{});
```

Here we constructed an anonymous object with the default constructor. Class templates are not types so we cannot create objects thereof:

Click here to view code image

```
template <typename Value>
struct power {
    Value operator() (Value x, Value y) const { return pow(x,
    y); }
};
```

```
functions.push_back(power{}); // Error
```

We can only construct objects from instantiated templates:

```
functions.push_back(power <double>{} );
```

8. Thus, they may have different signatures since equal function names aren't required. In contrast, the equality of signatures doesn't impose the same return types.

On the other hand, we can can create objects from classes that contain function templates:

Click here to view code image

```
struct greater_t {
    template <typename Value>
    Value operator() (Value x, Value y) const { return x > y;
    }
} greater_than ;
```

```
functions.push_back(greater_than);
```

In this context, the template call operator must be instantiatable for function type. As a counter-example, the following statement doesn't compile as we cannot instantiate it to a function with different argument types:

Click here to view code image

```
function<double(float, double)> ff = greater_than; // Error
```

Member functions can only be stored when they are static. In the following class: