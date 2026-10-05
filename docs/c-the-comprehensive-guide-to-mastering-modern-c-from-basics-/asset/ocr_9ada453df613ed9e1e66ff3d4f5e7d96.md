```
// https://godbolt.org/z/PGMPAbsKc
#include <fstream>
#include <iostream>
#include <vector>
using std::cout;
int main() {
    std::ofstream file("testfile.txt", std::ios::binary);
    if (!file) { /* Error */ << cout << "ERR1\n"; return 1; }
    std::ifstream filecopy("backup.dat", std::ios::binary);
    if (!filecopy) { /* Error */ << cout << "ERR1\n"; return 1; }
    file.seekg(0, std::ios::end);
    auto size = file.tell();
    cout << "size: " << size << " bytes\n";
    filecopy.seekg(0, std::ios::beg); // Important!
    std::vector<char> buffer(size);
    file.read(buffer.data(), size);
    if (!file) { cout << "Error reading...\n"; return 1; }
    cout << "Read: " << file.gcount() << " bytes\n";
    filecopy.write(buffer.data(), size);
    if (!filecopy) { cout << "Error writing...\n"; return 1; }
}
```

# Listing 27.22 Block-wise reading and writing with "read" and "write".

With file and filecopy, I first opened a file for reading and another file for writing to copy (both in binary mode with ios::binary). Then I set the position of the file to be copied to the end (ios::end) using the seekg() method. Using the position at the end of the file, I get the tellg() method and later store the size of the file in the size variable for copying.

It is also very important not that I reset the read position to the beginning with seekg. Then I get a sufficiently large buffer to read the entire file. For this, I initialize a vector of size size with elements of type char. A vector guarantees that all elements are stored consecutively in one block. This is useful and necessary to serve as a parameter for the following calls to read