# Sequence output

```
```cpp
// sequenceOutput.cpp

#include <syncstream>
#include <iostream>

int main() {

    std::ostringstream bout1(std::cout);
    bout1 << "Hello, ";
    {
        std::osyncstream(bout1.get_wrapped()) << "Goodbye, " << "Planet!" << '\n';
    } // emits the contents of the temporary buffer

    bout1 << "World!" << '\n';

} // emits the contents of bout1
```
```

![](bbox=[0.381, 0.439, 0.619, 0.498])

Synchronized access to `std::cout`