# **Unsafe comparison of integers resolved**

```
~~~cpp
// unsafeComparison2.cpp

int main() {
    int x = -3;
    unsigned int y = 7;

    bool val = x < y;
    static_assert(static_cast<unsigned int>(-3) == 4'294'967'293);
}
~~~
```

In the example, I'm focusing on the less-than operator. C++ Insights^11 gives me the following output:

```
~~~cpp
int main()
{
    int x = -3;
    unsigned int y = 7;
    bool val = static_cast<unsigned int>(x) < y;
    /* PASSED: static_assert(static_cast<long>(static_cast<unsigned int>(-3)) == 4294967293L); */
}
~~~
```

# **Unsafe comparison analyzed**

Here is what's happening:

+   - The compiler transforms the expression x < y (line 7) into static_cast<unsigned int>(x) < y. In particular, the signed x is converted to an unsigned int.
+   - Due to the conversion, -3 becomes 4'294'967'293.
+   - 4'294'967'293 is equal to -3 mod 2^32
+   - 32 is the number of bits of an unsigned int on C++ Insights.

Thanks to C++20, we have a safe comparison of integers.

# ### 5.4.1.2 Safe Comparison of Integers

C++20 supports six comparison functions for integers: