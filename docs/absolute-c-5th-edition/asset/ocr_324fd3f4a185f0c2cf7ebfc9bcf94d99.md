# I/O Streams 531

If there are no more numbers to be read in, then nothing is input and the Boolean variable false is returned, the loop ends. In this example the type of the input variable next was double, but this method of checking for the end of the file works the same way for other data types, such as int and char.

This second method of testing for the end of a file is preferred by many C++ programmers for what appears to be a cultural reason. It was commonly used in C programming. It is also possible that, depending on implementation details, this second method might be more efficient. In any event, whether you need to know it so you can understand other programmers' code, an illustration of the eof member function is given in Display 12.4.

# Display 12.4 Checking for the End of a File (part 1 of 2)

```
// story.txt to numstory.txt,
// adds a number to the beginning of each line.
//Assumes story.txt is not empty.
#include <fstream>
#include <iostream>
#include <cstdlib>

using std::ifstream;
using std::ostream;
using std::cout;

int main() 
{
    ifstream fin;
    ostream fout;

    fin.open("story.txt");
    if (fin.fail()) {
        cout << "Input file opening failed.\n";n        exit(1);
    }

    fout.open("numstory.txt");
    if (fout.fail()) {
        cout << "Output file opening failed.\n"
        exit(1);
    }
n
```

(continued)