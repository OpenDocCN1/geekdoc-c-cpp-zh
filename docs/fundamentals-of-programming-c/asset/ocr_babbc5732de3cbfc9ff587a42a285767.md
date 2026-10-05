# 19.4. CATCHING MULTIPLE EXCEPTIONS

```
Listing 19.8: fileareadmultiexcept2.cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <string>

using namespace std;

// Exception object to thrown when a client attempts to
// open a text file with a name that does correspond to a
// file in the current working directory.
class FileNotFoundException : public exception {
    string message; // Identifies the exception and filename
public:
    // Constructor establishes the exception's message
    FileNotFoundException(const string& fname)
        : message(\" + fname + "\n not found") {}

    // Reveal message to clients
    const char *what() const {
        return message.c_str();
    }
};

// Creates and returns a vector of integers from data stored
// in a text file.
// filename: the name of the text file containing the data
// Returns a vector containing the data, if possible
vector<int> load_vector(const string& filename) {
    ifstream fin(filename); // Open the text file for reading
    if (fin.good()) { // Did the open file successfully?
        int n;
        fin >> n; // Size of data set
        vector<int> result(n); // Allocate space for the vector
        int value, i = 0;
        while (fin >> value)
            result.push_back(value); // Append it to the vector
        fin.close(); // Close the file
        return result;
    } else // Could not open the text file
        throw FileNotFoundException(filename);
}

int main() {
    try {
        vector<int> numbers = load_vector("values.data");
        for (int value : numbers)
            cout << value << endl;
    } catch (out_of_range& e) {
        cout << "Error: vector bounds exceeded" << endl;
    }
}
```