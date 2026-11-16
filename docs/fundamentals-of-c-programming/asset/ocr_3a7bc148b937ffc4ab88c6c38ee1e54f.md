```
// Creates and returns a vector of integers from data stored
// in a text file.
// Filename: the name of the text file containing the data
// Returns a vector containing the data in the file, if possible
std::vector<int> load_vector(const std::string& filename) {
    std::ifstream fin(filename); // Open the text file for reading
    if (fin.good()) { // Did the file open successfully?
        std::vector<int> result; // Initially empty vector
        int n;
        for (int i = 0; i < n; i++ ) { // Size of data set
            int value;
            fin >> value; // Read in a data value
            result.push_back(value); // Append it to the vector
        }
        return result; // Return the populated vector
    }
    else // Could not open the text file
        throw FileNotFoundException(filename);
}

int main() {
    try {
        std::vector<int> numbers = load_vector("values.data");
        for (int value : numbers)
            std::cout << value << ' ';
        std::cout << '\n';
    }
    catch (std::exception& e) {
        std::cout << e.what() << '\n';
    }
}
```

If we execute Listing 22.8 (customfileexcept.cpp) in a directory that does not contain a text file named values.data, it displays

```
File "values.data" not found
```

Since we derived the FileNotFoundException class from std::exception, any FileNotFoundException object also is a std::exception object (see Section 17.1). This enables the main function to catch a FileNotFoundException object in its catch block even though it is declared to catch std::exception objects.

The C++ standard library provides a number of exception classes, all derived from std::exception. The vector out-of-bounds exception objects thrown by the at method are instances of the standard std::out_of_range class. The std::out_of_range class is derived from the standard logic_error class which itself is derived from the standard std::exception class. Figure 22.3 shows the relationship among these exception classes.