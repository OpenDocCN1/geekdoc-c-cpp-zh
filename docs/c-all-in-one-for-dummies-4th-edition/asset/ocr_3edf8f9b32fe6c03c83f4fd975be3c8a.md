you must change the `#include <optional>` to read `#include <experimental/optional>` because the support is experimental. There are other necessary changes as well, which you can see in the OptionalExperimental project in the downloadable source code.)

# **LISTING 8-12:** Using optional to Avoid Instances of Nothing

```
```cpp
#include <iostream>
#include <optional>

using namespace std;

void myFunction(optional<string> name = nullopt) {
    if (name == nullopt) {
        cout << "I wish I knew your name!" << endl;
    } else {
        cout << "Hello " << name.value() << "!" << endl;
    }
}

int main() {
    myFunction();
    myFunction("Sarah");
    return 0;
}
```
```

In this case, you see `myFunction()`, which accepts nothing or a string. If the caller sends nothing, then name equals `nullopt`. On the other hand, if the caller sends a string, the code uses `name.value()` to obtain the string and print it onscreen. Note that you can't access the string directly but must call `value()` instead. Here is the output from this example:

```
```
I wish I knew your name!
Hello Sarah!
```
```

![](bbox=[0.177, 0.697, 0.243, 0.747])

**WARNING**

You might be tempted to think that `nullopt` somehow equals `nullptr`. However, this isn't the case. If you try to replace the `nullopt` check in Listing 8-12 with `(ptr == nullptr)`, the compiler will complain loudly that you're using the wrong data type.