We can ignore elements in a std::tie function by using std::ignore as the element value.

# Unpacking A Tuple

We can also use std::tie to unpack a tuple into variables:

```
#include <iostream>
#include <string>
#include <tuple>

int main() {
    int x;
    std::string y;
    double z;

    std::tuple<int, std::string, double, int> mytuple;

    // assign to mytuple
mytuple = {5, "hello world", 90.67, 0};

    // unpack the tuple
    std::tie(x,y,z, std::ignore) = mytuple;

    std::cout << "x: " << x << std::endl;
    std::cout << "y: " << y << std::endl;
    std::cout << "z: " << z << std::endl;

    return 0;
}

# output
x: 5
y: hello world
z: 90.67
```