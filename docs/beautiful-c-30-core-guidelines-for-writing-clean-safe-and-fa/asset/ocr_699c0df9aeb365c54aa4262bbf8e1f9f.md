```
};
int main() {
    std::cout << sizeof(int_two_bools);
}
```

What answer would you expect to see?

We built and ran this program using x64 MSVC 19.28 on Compiler Explorer and got the answer 12. Each member takes up four bytes.

![](bbox=[0.12, 0.36, 0.4, 0.48])

Figure 2.4.1. Layout for storing an integer and two bools

Then we exchanged the second and third members, thus:

Click here to view code image

```
struct int_two_bools {
    bool m_b1;
    bool m_b2;
    int m_i;
};
```

Now what answer would you expect to see? You can check the output on Compiler Explorer and observe that the answer is 8.

![](bbox=[0.12, 0.93, 0.4, 0.98])

Figure 2.4.2. Optimized layout for storing an integer and two bools