```
```cpp
if (!file.is_open()) {
    throw std::runtime_error("Failed to open file");
}

}

~FileHandle() {
    file.close(); // Ensure file is always closed when the FileHandle object
                  // is destroyed
}

// Disable copy operations to ensure unique ownership of the resource

FileHandle(const FileHandle&) = delete;

FileHandle& operator=(const FileHandle&) = delete;

// Enable move operations for transfer of ownership
```
```