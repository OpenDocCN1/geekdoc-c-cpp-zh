```
multiply(z)
}
```

Both 5 and x are compile-time constants, so they can be used in the consteval function z is not a compile-time constant, therefore multiply(z) will not compile.

# constitut Variables

Global variables, static variables, static class members and thread-local variables have static storage duration. These objects are allocated when the program starts and deallocated when the program ends.

A variable with static storage may be initialized at (i) compile-time, or (ii) when the declaration is encountered at run-time (for example when a static variable is inside a function block).

A constit is a variable with static storage that is guaranteed to be initialized at compile-time. The constit attribute can only be applied to static storage variables.

A const variable is not necessarily a constit variable since it does not have to be initialized at compile-time.

# contexpr try-catch Blocks

C++20 allows try-catch blocks inside constexpr functions but throw is not allowed. The catch block in a constexpr function is simply ignored at compile-time.

```
constexpr void f(A_t x, A_t y){
  try{
    bool ret = (x == y);
    // ...
  }
```