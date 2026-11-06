# Storing in a vector

The Vectors example, shown in Listing 6-1, demonstrates how to use a container class. This particular container is a data type called a vector, and it works much like an array.

# LISTING 6-1: Using Vectors as Examples of Container Classes

```
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<string> names;

    names.push_back("Tom");
    names.push_back("Dick");
    names.push_back("Harry");
    names.push_back("April");
    names.push_back("May");
    names.push_back("June");

    cout << names[0] << endl;
    cout << names[5] << endl;
    return 0;
}
```
```

You use vector as a template. That means that it’s going to have a template parameter, which is string in this case. Note also the included header files. Among them are <vector> (with no .h after the filename). In general, you include the header file that matches the name of the container you are using. Thus, if there were such a thing as a container called rimbucklebock, you would type #include <rimbucklebock>. Or, if you use the container called set, you type #include <set>. When you run this example, you see two names as output:

```
Tom
June
```

There are a number of advantages to using a vector instead of a regular, plain old, no-frills array:

![](bbox=[0.174, 0.805, 0.239, 0.874])

> You don’t need to know up front how many items will be going in it. With an array, you need to know the size when you declare it.