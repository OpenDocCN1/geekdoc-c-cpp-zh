```
```cpp
int main() {
    // Declaration and initialization of an integer vector
    std::vector<int> dynamicVector = {1, 2, 3, 4, 5};

    // Modifying vector elements using a for loop
    for (int i = 0; i < dynamicVector.size(); ++i) {
        dynamicVector[i] = dynamicVector[i] * 2; // Doubling each element
    }

    // Displaying the modified vector
    for (int i = 0; i < dynamicVector.size(); ++i) {
        std::cout << "Modified Element " << i << ": " << dynamicVector[i] << std::endl;
    }

    return 0;
}
```
```

This example illustrates using a for loop to double the values of a vector and then displaying the modified elements.

Understanding the syntax and advantages of vectors in C++ opens up dynamic possibilities for managing collections of data with varying size requirements. Whether dynamically adding elements, resizing, or performing iterative manipulations, vectors provide a flexible and powerful solution for modern C++ programming.