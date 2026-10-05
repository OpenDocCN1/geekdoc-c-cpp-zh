**Table 4.11** Truth table for all Boolean expressions with two values.

It would actually be sufficient for the computer to output a b to store a bool. However, the computer actually uses at least one char and more often for int. This is because the computer always blocks an entire “memory word” when manipulating bits and would therefore slow down neighboring bits. So you spend a little more space on independence and respect.

If you want to save a large number of individual bools, you should take a look at the std::bitset data type in the standard library.

This relationship with int is one of the reasons that you can also simply use an int in tests with if and the like in C++:

```
int idx = 100;
while(idx) { // an int as a test
    readLine(line);
    --idx;
}
```