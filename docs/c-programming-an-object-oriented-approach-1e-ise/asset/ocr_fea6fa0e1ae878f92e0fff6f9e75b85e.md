We need to be careful about exceptions in constructors and destructors. If an object cannot be fully formed by the constructor, the corresponding destructor is not called. This can create a serious problem if the object is totally or partially created in the heap. Throwing an exception in this case may create a memory leak. To link the allocation and releasing of the memory together, we use a smart pointer instead of a raw pointer. The smart pointer allocates memory when its constructor is called and releases memory when its destructor is called. Standard exception classes are defined in the C++ library and are derived from the `exception` class. They are divided into `logical errors` and `run-time errors`.

# Problems

**PR-1.** What happens when the following short program is run?

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
    int value = 30;
    if (value > 20) throw value;
    cout << value;
    return 0;
}
```
```

**PR-2.** What happens when we try to compile the following short program?

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
    int value = 30;
    try
    {
        if (value > 30) throw value;
    }
    cout << value;
    return 0;
}
```
```

**PR-3.** What happens when the following short program is run?

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
    int value = 30;
    try
    {
        if (value < 20) throw value;
```
```