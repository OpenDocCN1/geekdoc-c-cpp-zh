example, it would be a built-in array of `double` values with `100` elements.

We could have used this technique in our `GradeBook` class of **Section 7.9**. Rather than defining `static` constants in the class definition’s body to represent the number of students and the number of tests, we could have defined class `GradeBook` as a class template with two nontype template parameters, as in

```
```cpp
template <size_t students, size_t tests>
class GradeBook {
    // class definition’s body
};
```
```

then used the nontype template parameters’ values throughout the class definition. We ask you to implement this version of class `GradeBook` in **Exercise 18.14**.