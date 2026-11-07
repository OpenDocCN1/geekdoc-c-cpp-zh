Doxygen simplifies the documentation process by extracting comments from the source code and producing well-structured documentation in various formats, such as HTML, LaTeX, or even plain text. To integrate Doxygen into a C++ project, developers need to create a configuration file, often named Doxyfile. This file contains project-specific settings and preferences for the documentation generation process.

```
```cpp
/**
 * @file main.cpp
 * @brief Example C++ program for Doxygen documentation.
 */

#include <iostream>

/**
 * @brief Function to calculate the square of a number.
 * @param x The input number.
 * @return The square of the input.
 */
int square(int x) {
    return x * x;
}

int main() {
    int result = square(4);

    // Displaying the result
    std::cout << "Square: " << result << std::endl;

    return 0;
}
```
```

In this example, comments above the function and main code block provide the necessary documentation for Doxygen to extract.

# ## Configuring Doxygen Settings

The Doxyfile configuration file allows developers to customize the documentation generation process. It includes settings such as input source files, output directory, and documentation format. Below are some key settings in a typical Doxyfile:

```
```text
# Specify the input source files or directories
INPUT = main.cpp

# Specify the output directory for generated documentation
```
```