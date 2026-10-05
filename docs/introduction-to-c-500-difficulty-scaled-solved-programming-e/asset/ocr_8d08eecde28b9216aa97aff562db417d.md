```
for (i = 0; i < 3; i++) {
    fout << "Hello " << i+1 << '\n';
    fout.close(); // Close the file.
    return 0;
}
```

The name of the object can be any C++ name (e.g., fout). When we open a file for writing in this way, the program creates the file, if it does not. If it exists, contents are deleted. Next, we'll see how to write to an existing file without deleting its contents.

If the file exists in the same folder with the executable program, we just put the file in double quotes. If it does not exist, the file is created in the same folder with the executable, then the full path must be specified.

If the operating system uses the character \ to specify the path, \\, as we saw in Chapter 3, C++ treats \ as an escaping escape sequence.

For example, if our program runs in Windows and we intend to write to the test.txt file that resides in the d:\dir\dir2 path, we should write:

```
fout.open("d:\dir\dir2\test.txt");
```

However, if the program obtains the file name from the command line, it is not needed to add an extra \. For example, we use d:\dir\dir2\test.txt.
With is_open() we check if the path is opened successfully. If not, the program terminates. For example, is_open() fails when the file path is invalid or we do not have permission to write to the file. Because ostream is derived from the ostream class, its objects can use the ostream functions, such as the overloaded operator<< functions.

If we want to associate the object with a different file we should first close the existing file. For example:

```
fout.close(); // Close the file.
fout.open("new.txt"); // Open a new file.
```

close() closes the file associated with the calling object. All data in memory is written to the file. Also, an open file closes the associated object ceases to exist, for example, when the program terminates.
Similarly, to the readers of a file, we need to create an istream object, associate it with the file, and use it, as we use cin, to read its contents. In the following example, suppose that each line of the input contains the temperatures of an array. A program reads and displays those within [–5,5].

```
#include <iostream> // Example 24.2
#include <fstream>
#include <string>
#include <cstdlib>
using namespace std;
```

```
int main() {
    double temp;
    string fname;
    cout << "Enter file name: ";
    cin >> fname;
}
```