# Instantiate function objects to use them

It's a common error that the name of the function object (`Square`) is used in an algorithm instead of the instance of function object (`Square()`) itself: `std::for_each(myVec.begin(), myVec.end(), Square)`. Of course, that's a typical error. You have to use the instance: `std::for_each(myVec.begin(), myVec.end(), Square())`

# 18.13 Lambda Functions

Lambda functions provide their functionality in-place. The compiler gets its information right on the spot and has therefore excellent optimization potential. Lambda functions can receive their arguments by value or by reference. They can capture the variables of their defining environment by value or by reference as well.

```
std::vector<int> myVec{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
std::for_each(myVec.begin(), myVec.end(), [](int& i){ i= i*i; });
                                // 1 4 9 16 25 36 49 64 81 100
```

# Lambda functions should be your first choice

If the functionality of your callable is short and self-explanatory, use a lambda function. A lambda function is generally faster than a function or a function object and easier to understand.

# 18.14 Lazy evaluation

In the case of lazy evaluation⁴, the expression is only evaluated if needed. This evaluation strategy is orthogonal to eager evaluation. Lazy evaluation is often called call-by-need.

# 18.15 Lock-free

A non-blocking algorithm is lock-free if there is guaranteed system-wide progress. The following algorithm incrementing the atomic counter is lock-free.