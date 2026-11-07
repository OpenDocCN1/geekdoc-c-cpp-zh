```
```cpp
};
```
```

# Usage example

```
```cpp
int main() {
    std::ofstream file("log.txt");

    DualStreamBuf dualBuf(std::cout, file);

    std::ostream dualStream(&dualBuf);

    dualStream << "Message logged to console and file\n";

    return 0;
}
```
```

This DualStreamBuf class directs output to two different stream objects, allowing simultaneous logging to the console and a file. By overriding it ensures that each character written to the stream is sent to both destinations.