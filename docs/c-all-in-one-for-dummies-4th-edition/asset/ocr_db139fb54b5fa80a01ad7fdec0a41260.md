# ### LISTING 2-3: Copying Structures Easily

```
```cpp
#include <iostream>

using namespace std;

struct Point3D {
    double x;
    double y;
    double z;
};

int main() {
    Point3D FirstPoint = { 10.5, 22.25, 30.8 };
    Point3D SecondPoint = FirstPoint;

    cout << SecondPoint.x << endl;
    cout << SecondPoint.y << endl;
    cout << SecondPoint.z << endl;
    return 0;
}
```
```

![](bbox=[0.172, 0.498, 0.233, 0.564])

Because structures are almost identical to classes, you can take Listing 2–2 and change the structure definition to the following class definition, and the application will continue to function the same:

```
```cpp
class Point3D {
  public:
    double x;
    double y;
    double z;
};
```
```

No matter which form of the application you use, the output is simple. When you run this application, you see output similar to this:

```
```
10.5
22.25
30.8
```
```

# ## Returning compound data types

Because simple structures are just a grouping of smaller data items, you can treat them as one chunk of data. For that reason, you can easily return them from