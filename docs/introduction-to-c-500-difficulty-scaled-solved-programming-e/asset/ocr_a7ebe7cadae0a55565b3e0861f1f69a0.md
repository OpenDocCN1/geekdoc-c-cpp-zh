What about if we only want to use the value of the argument and prevent any changes? You know the answer; we make the pointer const.

```
void test(const int *p, int a) // We also change the declaration.
{
    if(*p == 10) // Fine.
        *p = 30; // Error.
}
```

One example to test what you've learned so far. What is the output of the following program? Do not rush to see the answer on the next page. Easy, make no mistake.

```
#include <iostream> // Example 11.8
void test(int *arg);
int var = 100;

int main() {
    int *ptr, i = 30;
    ptr = &var;
    test(ptr);
    std::cout << *ptr << '\\n';
    return 0;
}

void test(int *arg) {
    arg = &var;
}
```