| Name | Expression | Description |
|---|---|---|
| phi | \(\varphi = (1 + \sqrt{5})/2\) | Golden ratio |

=> c++20/math_constant_examples.cpp

Using these constants allows us to write generic functions without conversion:

Click here to view code image

```
template <typename T>
T circular_area (T r)
{
    return std::numbers::pi_v <T> * r * r;
}
```

as demonstrated for the circular area.

# ## 4.3 Meta-programming

In this section, we will give you a foretaste of meta-programming. Here, we will focus on the library support and in Chapter 5 we will provide more background.

# ### 4.3.1 Limits

A very useful library for generic programming is <limits> which provides important information on types. It can also prevent surprising behavior when the source is compiled on another platform and some types are implemented differently. The header <limits> contains the class template numeric_limits that delivers type-specific information on intrinsic types. This is especially important when dealing with numeric type parameters.

In Section 1.7.5, we demonstrated that only some digits of floating-point numbers are written to the output. Especially when the numbers are written to files, we want to be able to read back the correct value. The number of decimal digits is given in numeric_limits as a compile-time constant. The