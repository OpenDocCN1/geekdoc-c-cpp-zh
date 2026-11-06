It looks like a function call or like the way you would declare a pointer variable, except there's no asterisk and no `new` word. It's actually a functional syntax for calling a constructor. The right side creates a new instance of `Simple`, passing 5 into the constructor. This new instance gets copied into the `inst` variable.

![](bbox=[0.17, 0.22, 0.25, 0.3])

This approach can be handy when you create an array of objects, where the array contains actual objects, not pointers to objects:

```
```cpp
Simple MyList[] = { Simple(1), Simple(50), Simple(80),
    Simple(100), Simple(150) };
```
```

The approach seems a little strange because the variable `MyList` is not a pointer, yet you're setting it equal to something on the right. But this approach is handy because you may need a temporary variable. The `Constructor05` example, shown in Listing 3-1, demonstrates how you can use the functional syntax to create a temporary instance of the class `string`.

# LISTING 3-1: Creating Temporary Instances with Functional Constructors

```
```cpp
#include <iostream>

using namespace std;

void WriteMe(string str) {
    cout << "Here I am: " << str << endl;
}

int main() {
    WriteMe(string("Sam"));
    return 0;
}
```
```

When you compile and run this, you see this output:

```
```text
Here I am: Sam
```
```

The code creates a temporary instance of the `string` class in `main()`. But as it turns out, an even shorter version of this code is available by calling `WriteMe()` like this:

```
```cpp
WriteMe("Sam");
```
```

This code works out well because you don't even feel like you're working with a class called `string`. The parameter just seems like a basic type, and you're passing

Constructors, Destructors, and Exceptions