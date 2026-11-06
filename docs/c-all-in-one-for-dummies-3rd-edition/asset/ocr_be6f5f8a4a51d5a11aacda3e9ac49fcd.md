![](bbox=[0.23, 0.135, 0.852, 0.492])

**Figure 6-1:** Configure Code::Blocks to allow use of new language features.

# **Listing 6-12: Creating and Using Dynamic Arrays**

```
```cpp
#include <iostream>
#include <new>

using namespace std;

int main()
{
    int HowMany;
    int* DynArray;

    cout << "How many numbers would you like?" << endl;
    cin >> HowMany;

    DynArray = new (nothrow) int[HowMany];
    if (DynArray == nullptr)
        cout << "Error: Could not allocate memory!";
    else
    {
        for (int i = 0; i < HowMany; i++)
            DynArray[i] = i;

        cout << "Displaying entries:" << endl;
        for (int i = 0; i < HowMany; i++)
            cout << DynArray[i] << endl;

        delete[] DynArray;
    }
    return 0;
}
```
```