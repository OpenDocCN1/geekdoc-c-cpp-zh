![](bbox=[0.235, 0.181, 0.647, 0.472])

*Figure 19-1. Execution of an expression using a function pointer*

# ## Callback Functions for Higher-Order Functions

*Pointer to function* is a perfectly reasonable type, which means a function can have a parameter of this type as well. The function can then use its pointer to function parameter to call the function to which the argument points when the function is called. You can specify just a function name as the argument for a parameter that is a "pointer to function" type. A function passed to another function as an argument is referred to as a *callback function*; the function that accepts another function as an argument is a *higher-order function*. Consider the following example:

```
```cpp
// Optimum.cpp - a function template to determine the optimum element in a given vector
export module optimum;
import <vector>;

export template <typename T>
const T* findOptimum(const std::vector<T>& values, bool (*compare)(const T&, const T&))
{
  if (values.empty()) return nullptr;
```
```