```
```cpp
for (int n = 0; n<number; ++n)
{
    std::cout << generator2() << ", ";
}
std::cout << "\\n";
```
```

We got the following output when we ran this code:

3224128699, 1790518196, 367697637, 3964670867,

1545172431, 2759616371, 502877303, 3738674815,

For completeness, we give some examples of std::seed_seq producing values that are distributed over an entire 32-bit range. This provides a way to seed a large number of random number engines or to seed a generator that requires a lot of entropy, given a small seed or a poorly distributed initial seed sequence:

```
```cpp
void SeedSequence()
{
    // Initial seed sequence of length 0
    std::seed_seq s1;

    // Iterate over a range
    int a[4] = { 1,2,3,4 };
    std::seed_seq s2(a, a + 4);

    // Initialiser list
    std::seed_seq s3 = { -1,0, 1 };
}
```
```

# A1.7 SUMMARY AND CONCLUSIONS

In this appendix we gave an overview of the *Boost Multiprecision* library. It has support for high-precision integral and floating-point data types. It is possible to carry out the usual arithmetic operations on these types and the common mathematical functions in the namespace std (the <cmath> library) have their equivalents in the namespace boost::multiprecision. We also discussed how to integrate multiprecision data types with a number of C++ language features and libraries that we discussed in previous chapters.

In most applications it will probably not be necessary to use multiprecision data types unless you are experiencing underflow or overflow problems. The price for the added robustness is a reduction in performance in general.

# A1.8 EXERCISES AND PROJECTS

+   1. **(Stiff ODEs and Multiprecision)**
+   
+      We have seen in Chapter 24 that explicit finite schemes (such as the Euler and Runge–Kutta methods) perform badly for ODEs with *several time scales*. The objective