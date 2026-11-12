A function call, resolved at compile time, is called early binding and any direct function call is a simple example for the early binding.

# 139. Write on the access rights with all kinds of inheritances.

The following diagram is sufficient to get the clarity.

![](bbox=[0.155, 0.295, 0.425, 0.523])

# 140. How can someone make a function pure virtual function?

a. Option one, the function can be assigned to 0 hence, it becomes a pure virtual function.

```
```cpp
#include <iostream>
using namespace std;
class Base_class
{
public:
    virtual void show() = 0;
};
```
```

b. the below shown example is not a mostly preferred way. But still, it would work like pure virtual function.

```
```cpp
#include <iostream>
using namespace std;
```
```

```
```cpp
class Base_class
{
public:
    virtual void show()
    { // Nothing inside. Hence,
      it is also performing pure
      virtual function's
      functionality.
    }
};
```
```

# 141. What are the restrictions one needs to understand when making a function pure virtual with { } instead of assigning the function to 0?

When one uses { } instead of assigning 0, creation of object is permitted which is actually to be avoided. An object cannot be created for an abstract class.

# 142. What are the classes involved in file handling?

The three major classes involved in file handling are:

+   - ✓ ofstream: Class for writing into the files.
+   - ✓ ifstream: Class for reading from the files.
+   - ✓ fstream: class to both read and write from/to files.

# 143. What are the modes a file can be opened in C++?

A file can be opened in any of the following modes:

+   - ✓ ios::app
+   - ✓ ios::ate
+   - ✓ ios::binary
+   - ✓ ios::in
+   - ✓ ios::out
+   - ✓ ios::nocreate
+   - ✓ ios::noreplace
+   - ✓ ios::trunc