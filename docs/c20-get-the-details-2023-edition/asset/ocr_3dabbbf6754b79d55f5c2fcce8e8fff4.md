```
```cpp
}
```
```

Function `lambdaGeneric` (line 9) can be invoked with any data type having a member function `size()`. Function `lambdaVector` (line 10) is more specific: it only accepts a `std::vector`. Function `lambdaVectorIntegral` (line 11) uses the C++20 concept `std::integral`. Consequently, it only accepts a `std::vector` using integral types such as `int`. To use the concept `std::integral`, I have to include the header `<concepts>`. I assume the small program is self-explanatory.

```
```text
lambdaGeneric(deq): 3

lambdaGeneric(vecDouble): 4
lambdaVector(vecDouble): 4

lambdaGeneric(vecInt): 5
lambdaVector(vecInt): 5
lambdaVectorIntegral(vecInt): 5
```
```

Lambdas, accepting a container and a `std::vector`

![](bbox=[0.117, 0.5, 0.179, 0.544])

# Class Template Argument Deduction

There is one feature in the program `templateLambdaVector.cpp` that you have probably missed. Since C++17, the compiler can deduce the type of a class template from its arguments (lines 20 - 22). Consequently, instead of the verbose `std::vector<int> myVec{1, 2, 3}`, you can simply write `std::vector myVec{1, 2, 3}`.

# 4.7.2 Detection of the Implicit Copy of the `this` Pointer

The C++20 compiler detects when you implicitly copy the `this` pointer. Implicitly capturing the `this` pointer by copy can cause undefined behavior. Undefined behavior essentially means that there are no guarantees about the program’s behavior, such as for the following: