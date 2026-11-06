# C++14 Binary Literals

As of C++14, you may now include `binary literals` in your source code. To do so, precede a sequence of 1s and 0s with `0b` or `0B`. For example, you can define a 32-bit mask like the one we used in the `displayBits` functions of this section’s examples as

```
```cpp
0b10000000'10000000'00000000'00000000
```
```

The preceding literal also uses C++14’s single-quote character to separate groups of digits for readability.