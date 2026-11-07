```
```cpp
#include

void printVersion(int version) {

assert(version > 0 && "Version must be positive"); // The program will
terminate if version is not positive

std::cout << "GitforGits version " << version << std::endl;

}

int main() {

printVersion(20); // Correct usage

//printVersion(-1); // Uncommenting this line will cause the assertion
to fail

return 0;

}
```
```