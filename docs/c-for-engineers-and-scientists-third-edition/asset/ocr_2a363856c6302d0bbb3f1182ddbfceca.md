# 402 Arrays

# Program 7.9

```
#include <iostream>
using namespace std;

int main() {
    const int NUMBELS = 20;
    int arr[NUMBELS];

    cout << "The starting address of the array is: " <<
         << &arr[0] << endl;
    cout << "The storage size of each array element is: " <<
         << sizeof(int) << endl;
    cout << "The address of element number 5 is: " <<
         << &arr[5] << endl;
    cout << "The starting address of the array, " <<
         << "\ndisplayed using the notation arr, is: " <<
         << int (arr) << endl;

    return 0;
}
```

Here is a sample output produced by Program 7.9:

The starting address of the array is: 1244796
The storage size of each array element is: 4
The address of element number 5 is: 1244816
The starting address of the array,
displayed using the notation arr, is: 1244796

Notice that the addresses have been displayed in decimal form, and element 5 is 20 bytes beyond the array's starting address. Also, the array's starting address is the same as the address of element 0, which is coded as &arr[0]. Alternatively, the starting address can also be obtained as arr, which is the array name, because an array name is a pointer constant, which is an address. (Chapter 12 explains the close association of array names and pointers.)
ray names and pointers.)