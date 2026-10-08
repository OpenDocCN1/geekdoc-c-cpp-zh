# Return Type

In many cases, you can skip the return type of the lambda and then the compiler will deduce the typename for you.

Initially, return type deduction was restricted to lambdas with bodies containing a single return statement. However, this restriction was quickly lifted as there were no issues with implementing a more convenient version.

C++ Standard Core Language Defect Reports and Accepted Issues 5

To sum up, since C++11, the compiler will be able to deduce the return type as long as all of your return statements are of the same type.

| If all rvalue return an expression and the types of the return expressions after lvalue-to-rvalue conversion (7.1 [conv.val]), array-to-pointer conversion (7.2 [conv.array]), and function-to-pointer conversion (7.3 [conv.func]) are the same, common type |

Return Type Deduction. Live code @Wandbox

```
#include <traits>
int main () {
    const auto baz = [[](int x) noexcept {
        if (x < 20)
            return x * 1.1;
        else
            return x * 2.1;
    }];
    static_assert(std::is_same<double, decltype(baz(10))::value,
        "has to be the same!");
}
```

In the above lambda, we have two return statements, but they all point to double so the compiler can deduce the type.

> In C++14 return type of lambda will be updated to adapt to the rules of auto deduction for regular functions. See this section.

# Trailing Return Type Syntax