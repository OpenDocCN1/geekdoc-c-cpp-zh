# 11.2. ARRAYS

```
cout << elem << ' ';
cout << endl;
}
```

Notice that this code does not involve using arrays at all! This code takes advantage of pointer arithmetic. If elem is a pointer to a value in memory, the expression elem++ makes point to the next location in memory that can store the value to which elem points. Since the memory devoted to an array is a continuous, block of memory addresses, pointer arithmetic simply redirects a pointer from one element to another element in that array. Listing 11.11 (pointerarithmetic.cpp) provides some example of pointer arithmetic.

# Listing 11.11: pointerarithmetic.cpp

```
#include <iostream>
using namespace std;

int main() {
    // Make an array
    int arr[] = {10, 20, 30, 40, 50};
    int *p = arr; // p points to the first element
    cout << p << endl; // Prints address, does not change p
    cout << p[0] << endl; // Prints 10, does not change p
    cout << p[1] << endl; // Prints 20, does not change p
    cout << ++p << endl; // Prints 20, does not change p
    p++; // Advances to the next element
    cout << ++p << endl; // Prints 30, does not change p
    p += 2; // Advance two places
    cout << +p[0] << endl; // Prints 40, does not change p
    cout << p[1] << endl; // Prints 50, does not change p
    p--; // Moves p back one place
    cout << ++p << endl; // Prints 30, does not change p
}
```

Listing 11.11 (pointerarithmetic.cpp) shows how a programmer can initialize all the elements in an array using a syntax similar to vector initializer list. Listing 11.11 (pointerarithmetic.cpp) prints

![](bbox=[0.148, 0.673, 0.781, 0.833])

Figure 11.7 illustrates how Listing 11.11 (pointerarithmetic.cpp) works. Also shows how we can use the square bracket array operator with a pointer. The expression p[i] refers to the element in memory i from the location pointed to by p.