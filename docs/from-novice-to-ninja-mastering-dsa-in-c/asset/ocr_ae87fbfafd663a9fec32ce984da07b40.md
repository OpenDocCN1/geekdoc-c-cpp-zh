```
std::cout << "Resource released." << std::endl;
}
};

int main() {
    try {
        // Acquire a resource using smart pointers
        std::unique_ptr<Resource> resource =
std::make_unique<Resource>();

        // Code that may throw exceptions

    } catch (const std::exception& e) {
        std::cerr << "Exception caught: " << e.what() <<
std::endl;
    }

    // Resource is automatically released when it goes out of
scope

    return 0;
}
```

Here, the Resource class acquires and releases a resource in its constructor and destructor, respectively. The use of smart pointers ensures proper resource cleanup even in the presence of exceptions.

Exception handling in C++ provides a powerful mechanism for dealing with errors in a structured and maintainable manner.

# Standard Template Library (STL): Harnessing the Power of Containers and Algorithms

The Standard Template Library (STL) is a powerful collection of C++ template classes and functions that provides generic, efficient, and versatile components. It consists of several components, including containers, algorithms, iterators, and function objects, making it a cornerstone of modern C++ development.

# Containers:

Containers are fundamental data structures provided by the STL, offering dynamic memory management and various methods to manipulate stored elements. Some commonly used containers include :-