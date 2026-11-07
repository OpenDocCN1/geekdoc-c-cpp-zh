```
```cpp
FileHandle(FileHandle&& other) noexcept : file(std::move(other.file))
{}

FileHandle& operator=(FileHandle&& other) noexcept {

    file = std::move(other.file);

    return *this;

}

std::fstream& get() { return file; }

};

void useFile(const std::string& path) {

    FileHandle fileHandle(path); // File is opened

    // Use the file

    fileHandle.get() << "Hello, RAII!" << std::endl;
```
```