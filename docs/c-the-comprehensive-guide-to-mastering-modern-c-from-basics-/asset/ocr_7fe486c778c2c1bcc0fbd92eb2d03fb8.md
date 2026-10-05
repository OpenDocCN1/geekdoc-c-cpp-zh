result at translation time but when the computation would cost runtime. However, whether the compiler actually precomputes the result in the described manner is still up to it.

With constexpr, you can define your own literal data types, as you can see in Chapter 23, Section 23.7.

The highest form for the ultimate minimal time consumption when running the program is consteval modifier for immediate functions introduced in C++20. This ensures that the compiler can compute an expression at translation time and insert it at the call site: as always, it doesn't have to, but it is likely. You can learn more about consteval in Chapter 13, Section 13.10.8.

# 7.12.4  Deleted Functions

If you want to prohibit use of a function, you can write = delete

instead of the function body:

```
double add(double a, double b) { return a + b; }
double add(int, int) = delete;    // prohibit add(3,4)
```

Without the second line with = delete, the compiler would automatically convert 3 and 4 to double. By making the declaration for add(int,int) known to it, it then chooses this one. However, by using = delete, you tell the compiler that you explicitly not want this behavior, and it will issue an error message.

# 7.12.5  Specialties in Class Methods

For functions that are part