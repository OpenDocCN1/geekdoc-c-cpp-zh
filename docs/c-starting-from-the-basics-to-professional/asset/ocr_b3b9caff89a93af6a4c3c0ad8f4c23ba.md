This works in essentially the same way as `smallest()`. We could use a function that scales the array elements by dividing by a given value:

```
```cpp
double* scale_range(double data[], size_t count, double divisor)
{
    if (!divisor) return data;    // Do nothing for a zero divisor

    for (size_t i {}; i < count; ++i)
        data[i] /= divisor;
    return data;
}
```
```

Dividing by zero would be a disaster, so when the third argument is zero, the function just returns the original array. We can use this function in combination with `largest()` to scale the elements that are now from 0 to some maximum to the range 0 to 1:

```
```cpp
scale_range(samples, count, *largest(samples, count));
```
```

Of course, what the user would probably prefer is a function that will normalize an array of values, thus avoiding the need to get into the gory details:

```
```cpp
double* normalize_range(double data[], size_t count)
{
    shift_range(data, count, -(smallest(data, count)));
    return scale_range(data, count, *largest(data, count));
}
```
```

Let’s see if it all works in practice:

```
```cpp
// Ex8_13.cpp
// Returning a pointer
import <iostream>;
import <format>;        // for std::size()
import <array>;
import <string>;

void show_data(const double data[], size_t count = 1,
               const std::string& title = "Data Values",
               size_t width = 10, size_t precision = 5);
const double* largest(const double data[], size_t count);
const double* smallest(const double data[], size_t count);
double* shift_range(double data[], size_t count, double delta);
double* scale_range(double data[], size_t count, double divisor);
double* normalize_range(double data[], size_t count);

int main()
{
    double samples[] {
                    11.0, 23.0, 13.0,  4.0,
                    57.0, 36.0, 317.0, 88.0,
```
```