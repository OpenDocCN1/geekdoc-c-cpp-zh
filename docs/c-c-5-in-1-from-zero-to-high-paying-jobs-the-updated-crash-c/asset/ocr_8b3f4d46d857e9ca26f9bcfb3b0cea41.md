```
#include <fstream>

int main() {
    std::ofstream outputFile;
    outputFile.open("output.txt");

    // Write data to outputFile

    outputFile.close();
    return 0;
}
```

# Formatting and Manipulating Input/Output Streams:

# Stream Manipulation:

The `<iomanip>` library provides tools for formatting output streams, like setting field width, precision, and alignment.

```
#include <iostream>
#include <iomanip>

int main() {
    double num = 3.14159;
    std::cout << std::fixed << std::setprecision(2) << num; // Outputs: 3.14
    return 0;
}
```

# Reading and Writing Structured Data Using Formatted I/O:

# Formatted Output:

You can use stream insertion (`<<`) to output structured data, like variables and text, to a file.