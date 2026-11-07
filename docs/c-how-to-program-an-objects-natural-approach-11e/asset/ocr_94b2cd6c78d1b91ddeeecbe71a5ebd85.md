that sort should use the default binary predicate function specified in sort’s definition—that is, `std::ranges::less`. This causes sort to arrange the elements in ascending order. The less function object compares its two arguments and returns true if the first is less than the second. If less returns false, the two salaries are not in ascending order, so sort reorders the corresponding Employee objects.

+   - The last argument specifies the **projection**. This unary function receives an element from the range and returns a portion of that element. Here, we implemented the unary function as a lambda that returns its Employee argument’s salary. The **projection** is applied *before* sort compares the elements, so rather than comparing entire Employee objects to determine their sort order, sort compares only the Employees’ salaries.

```
```cpp
// sort Employees by salary; {} indicates that the algorithm should
// use its default comparison function.
std::ranges::sort(employees, {},
    [](const auto& e) { return e.getSalary(); });
std::cout << "\nEmployees sorted in ascending order by salary:\n";
std::ranges::copy(employees, output);
```
```

```
```text
Employees sorted in ascending order by salary:
Makaya   Titania  3587
Wu       Joo-won  5000
Jones    Amaia    7600
```
```

# Shorthand Notation for a Projection

We can replace the unary function that we implemented as a lambda in line 46 with the shorthand notation

```
```cpp
&Employee::getSalary
```
```

This creates a pointer to the Employee class’s getSalary member function, shortening lines 45–46 to

```
```cpp
std::ranges::sort(employees, {}, &Employee::getSalary);
```
```

To be used as a projection, the member function must be public and must not be overloaded. Also, it must have no parameters because the `std::ranges` algorithms cannot receive additional arguments to pass to the member function specified in the projection.³²

# A Projection Can Be a Pointer to a public Data Member

If a class has a public data member, you can pass a pointer to it as the projection argument. For example, if our Employee class had a public data member named salary, we could specify sort’s projection argument as

```
```cpp
&Employee::salary
```
```

32. “Under the hood,” `std::ranges::sort` uses the `std::invoke` function (header `<functional>`) to call the provided comparator on each Employee object.