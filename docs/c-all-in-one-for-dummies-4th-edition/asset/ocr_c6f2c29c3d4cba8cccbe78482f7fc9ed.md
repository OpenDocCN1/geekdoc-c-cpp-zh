Each person gets a different class that reflects the maximum price they’re willing to pay. You can see that Fred gets a class called `PriceController<FredMaxPrice>`. Julie, however, gets a class called `PriceController<JulieMaxPrice>`. And remember, these really are different classes. The compiler created two different classes, one for each item passed in as a template parameter. Also notice that the parameters are constant integer values. `FredMaxPrice` is a constant integer holding 30. `JulieMaxPrice` is a constant integer holding 60.

For the first one, `PriceController <FredMaxPrice>`, the code creates two instances. For the second one, `PriceController <JulieMaxPrice>`, the code creates one instance. In all instances, the code sets the price of the item and then calls `TestPrice()` with the item name. If the item is too expensive, the `PriceController` outputs a special message. Here’s the output from this example:

```
    2
    Drawing set too expensive!
    Car too expensive!
```

![](bbox=[0.173, 0.419, 0.237, 0.488])

When working with some older versions of C++, you can’t use certain types, such as `float`, for your template. Doing so can cause the build process to fail with all sorts of odd messages. However, you also see the following message, which tells you precisely where the problem lies:

```
    'error': 'float' is not a valid type for a template non-type
        parameter
```

![](bbox=[0.173, 0.554, 0.237, 0.619])

Starting with C++ 11, you can use `std::nullptr_t;` as a parameter type, as in `template <std::nullptr_t N>`. When working with C++ 20, you gain access to these types as well:

+   - Floating-point type
+   - Literal class type with the following properties:
+     - All base classes and nonstatic data members are public and non-mutable.
+     - The types of all base classes and non-static data members are structural types. Depending on the compiler, you might also be able to use a multidimensional array of the structural type.

![](bbox=[0.173, 0.803, 0.237, 0.868])

A null pointer represents a special case that differentiates between `0` and an actual null (missing) value. Its actual representation is `(void *)0`, which makes it different from the C/C++ `NULL` value. You can see the null pointer discussed at https://hackeron.com/what-exactly-is-nullptr-in-c=-c94d636t and https://stackoverflow.com/questions/1365349/what-is-a-proper-use-case-of-std::nullptr_t-template-parameters.

# Creating Classes with Templates