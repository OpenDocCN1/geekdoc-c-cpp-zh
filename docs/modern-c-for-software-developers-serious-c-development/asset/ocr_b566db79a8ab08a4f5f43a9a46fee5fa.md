```
#include <iostream>

int main() {
    int x = 5;
    int *ptr1;
    int **ptr2;

    ptr1 = &x;
    ptr2 = &ptr1;

    int z = **ptr2;
    std::cout << z << std::endl;
}
```

# result

5