```
```cpp
[](auto i) { cout << i * 2 << " "; }
```
```

is a *lambda expression* that performs the multiplication and output.

Lambdas begin with the **lambda introducer** (`[]`), followed by a parameter list and function body. A lambda can use local variables from the function in which the lambda is defined. The introducer enables you to specify which, if any, local variables the lambda uses—this is known as **capturing** the variables. The empty lambda introducer (`[]`) in line 20 indicates that the lambda does not use any of `main`’s local variables.

The lambda in line 20 receives one parameter named `i`. Specifying the parameter’s type as `auto` enables the compiler to **infer** the parameter’s type, based on the context in which the lambda appears. In this case, the `for_each` algorithm calls line 20’s lambda once for each element of the `array`, passing the element’s value as the lambda’s argument. Since the `array` contains `int`s, the compiler infers parameter `i`’s type as `int`. Using `auto` to infer the parameter type is a new C++14 feature of so-called **generic lambdas**. In C++11 you were required to state each lambda parameter’s explicit type. In this example, the lambda in line 20 is similar to the standalone function