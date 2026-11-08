```
    std::cout << '\n';
    }
```

Here is the output of the program with the MSVC compiler.

![](bbox=[0.255, 0.252, 0.738, 0.576])

Use of all mathematical constants

The mathematical constants are available for float, double, and long double. By default, double is used but, you can also specify float (std::numbers::pi_v<float>) or long double (std::numbers::pi_v<long double>).

# ### 5.4.3 Midpoint and Linear Interpolation

+   - std::midpoint(a, b): calculates the midpoint (a + (b - a) / 2) of integers, floating points, or pointers. If a and b are pointers, they have to point to the same array object. The function needs the header <numeric>.
+   - std::lerp(a, b, t): calculates the linear interpolation (a + t(b - a)). When t is outside the range [0, 1], it calculates the linear extrapolation. The function needs the header <cmath>.

The program midpointLerp.cpp applies both functions.