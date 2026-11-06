that works with the object at a low level. However, the function may not have the resources or information to handle the exception, so it rethrows the exception to a function higher up that may have the required access. The calling function might have a `try...catch` block that can actually handle the exception. In other words, you might have something like the code found in the `Exception02` example:

```
```cpp
#include <iostream>

using namespace std;

void Inner() {
    throw string("Error!");
}

void Outer() {
    try {
        Inner();
    } catch (string excep) {
        cout << "Outer caught an exception: ";
        cout << excep << endl;
        throw;
    }
}

int main()
{
    try {
        Outer();
    } catch (string excep) {
        cout << "main caught an exception: ";
        cout << excep << endl;
    }
    return 0;
}
```
```

In the preceding code, `main()` calls `Outer()`. `Outer()`, in turn, calls `Inner()`. `Inner()` throws an exception, and `Outer()` catches it. But `main()` also wants to catch the exception. So `Outer()` rethrows the exception. You do that by calling `throw` without anything after it, like this:

```
```cpp
throw;
```
```

When you run this application, you see the following output.

```
```
Outer caught an exception: Error!
main caught an exception: Error!
```
```