```
o1 == 42        // yields true
o0 < o1        // yields true
```

This means that for optional objects of unsigned int, there is a value less than 0:

```
std::optional<unsigned> uo;
    uo < 0        // yields true
    uo < -42      // yields true
```

and for optional objects of bool, there is a value less than false:

```
std::optional<bool> bo;
    bo < false      // yields true
```

To make your code more readable, you should use

```
if (!uo.has_value())
```

instead of

```
if (uo < 0)
```

Mixed-type comparisons that use an optional object and the underlying type are supported provided the underlying types support them:

```
std::optional<int> o1{42};
std::optional<double> o2{42.0};
```

```
o2 == 42      // yields true
o1 == o2      // yields true
```

If the underlying type supports implicit type conversions, the mixed-type comparisons may also use implicit type conversions.

Note that optional Boolean or raw pointer values can result in some surprises.

# Changing the Value

Assignment and emplace() operations exist corresponding to the initializations:

```
std::optional<std::complex<double>> o;  // has no value
std::optional ox{77}; // optional<int> with value 77
```

```
o = 42;               // value becomes complex(42.0, 0.0)
o = {9.9, 4.4};        // value becomes complex(9.9, 4.4)
o = ox;               // OK, because int converts to complex<double>
o = std::nullopt;     // o no longer has a value
o.emplace(5.5, 7.7);  // value becomes complex(5.5, 7.7)
```

Assigning std::nullopt removes the value, which calls the destructor of the contained type if there was a value before. You can get the same effect by calling reset():

```
o.reset();            // o no longer has a value
```

or assigning empty curly braces:

```
o = {};               // o no longer has a value
```