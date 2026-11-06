![](bbox=[0.128, 0.116, 0.229, 0.189])

Just as the parameters to a function are normally values, a function normally *returns* a value. In the case of returning a pointer, the function is still returning just a value — it is returning the value of the pointer, which is a number representing an address.

# Returning a Pointer as a Nonpointer

You may find it annoying to dereference a pointer returned from a function every time you want to use it. Listing 7-14, in the preceding section, is an example of how you need to dereference a pointer each time. But you can avoid this issue by dereferencing the pointer as soon as it comes cranking out of the machine. The ReturnPointer2 example, shown in Listing 7-15, demonstrates: You precede the call to the function with an asterisk, which dereferences the result immediately. You then place the result in a local nonpointer variable. After that, you have the value in the variable, and you don't need to dereference the pointer when you want to use the value. Thus, when you call cout, you just use the variable directly without the use of asterisks and other pointer paraphernalia.

# **Listing 7-15: Dereferencing Your Return Value Immediately So You Don't Need to Use It as a Pointer**

```
```cpp
#include <iostream>

using namespace std;

string *GetNotSoSecretCode()
{
    string *code = new string("ABCDEF");
    return code;
}

int main()
{
    string newcode;
    int index;

    for (index = 0; index < 10; index++)
    {
        newcode = *GetNotSoSecretCode();
        cout << newcode << endl;
    }

    return 0;
}
```
```