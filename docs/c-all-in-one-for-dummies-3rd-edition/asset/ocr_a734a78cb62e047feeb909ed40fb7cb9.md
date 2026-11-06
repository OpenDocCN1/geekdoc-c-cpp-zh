where Numbers is an array of integers, you can access the element at Numbers[5] by dereferencing the pointer, as in

```
```cpp
cout << *cur << endl;
```
```

Then you can add and subtract numbers from the pointer, like these lines:

```
```cpp
cur++;
cout << *cur << endl;
```
```

The compiler knows how much memory space each array element takes. When you add 1 to cur, *it advances to the next element in the array*. And so the cout that follows prints the next element — in this case, Numbers[6].

The PointerArithmetic example, shown in Listing 9-11, shows how to move about an array. Note that we declare a variable called cur, which is a pointer to an integer. The array holds integers, so this pointer can point to elements in the array.

We start out with cur pointing to the first element. The array name is the address of the first element; to accomplish that, we simply typed

```
```cpp
cur = Numbers;
```
```

This line puts the address of the first element of the array in the variable cur.

# **Listing 9-11: Moving by Using Pointer Arithmetic**

```
```cpp
#include <iostream>

using namespace std;

int main()
{
    int Numbers[100];

    for (int i=0; i<100; i++)
    {
        Numbers[i] = i * 10;
    }

    int *cur;
    cur = Numbers;

    cout << *cur << endl;
    cur++;
    cout << *cur << endl;
    cur++;
    cout << *cur << endl;
    cur += 3;
    cout << *cur << endl;
    cur--;
    cout << *cur << endl;

    return 0;
}
```
```