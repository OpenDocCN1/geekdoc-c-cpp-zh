# Basic Operations with

Creating Directories: To organize user data or application logs.

```
```cpp
#include

#include

namespace fs = std::filesystem;

int main() {

fs::path dirPath = "GitforGitsData";

if(!fs::exists(dirPath)) {

fs::create_directory(dirPath);

std::cout << "Directory created: " << dirPath << std::endl;

}
```
```