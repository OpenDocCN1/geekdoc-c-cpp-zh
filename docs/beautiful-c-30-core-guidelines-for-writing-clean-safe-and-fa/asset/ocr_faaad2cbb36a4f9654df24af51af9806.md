them. This made returning objects a much more attractive proposition because the move constructor would be invoked to return something, so even if elision didn’t take place, at least the cost could be reduced and copying containers would be cheap.

Heroic efforts have been made to update the standard so that returning objects is as cheap as possible as often as possible. Since C++17, compilers are required to omit the copy and move construction of class objects, even if that means omitting observable side effects, in a return statement when the object being returned is a prvalue of the same type as the function return type. Before C++17 this was existing practice in most compilers, but standardizing this practice reassures the user.

This means that RVO is a safe bet, and you should always make heroic efforts to ensure that you return objects from a function as a constructor invocation, as in the RVO example above. You may have also seen return invoked with an initialization list:

Click here to view code image

```
```cpp
std::pair<int, int> f(int a, int b) {
    return {a + b, a * b};
}
```
```

This is also a prvalue and will enable the compiler to generate RVO-flavored code. NRVO is not required, since the object has no name. This requirement is not attached to optimizations or compiler flags: this will Just Happen, due to fundamental changes in C++17 to the specification of temporary values and prvalues.

This can trip up old coders (whistles innocently) because it means the compiler will prefer elision to side effects, so if you log things in move constructors or destructors you may be surprised by their nonappearance. However, this is the right thing for the standard to prefer and is in line with the goal of C++ to offer zero-overhead abstraction. Performance opportunities should not be avoided lightly.

# You can also return a tuple