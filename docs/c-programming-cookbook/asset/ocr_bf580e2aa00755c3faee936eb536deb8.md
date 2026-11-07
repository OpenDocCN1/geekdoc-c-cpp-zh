```
```cpp
void writeToTextFile(const std::string& filename, const std::string& content) {

    std::ofstream file(filename);

    file << content;

}

std::string readFromTextFile(const std::string& filename) {

    std::ifstream file(filename);

    std::string content((std::istreambuf_iterator(file)),
                        std::istreambuf_iterator());

    return content;

}
```
```