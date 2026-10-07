# Listing 17.17 count.cpp

```
// count.cpp -- counting characters in a list of files
#include <iostream>
#include <fstream>
#include <cstdlib> // for exit()
int main(int argc, char * argv[])
{
    using namespace std;
    if (argc == 1) { // quit if no arguments
        cerr << "Usage: " << argv[0] << " " << filename[s]\n";
        exit(EXIT_FAILURE);
    }

    ifstream fin; // open stream
    long count;
    long total = 0;
    char ch;

    for (int i = 1; i < argc; file++) {
        fin.open(argv[file]); // connect stream to argv[file]
        if (!fin.is_open()) {
            cerr << "Could not open " << argv[file] << endl;
            fin.clear();
            continue;
        }
        count = 0;
        while (fin.get(ch)) {
            count++;
        }
        cout << count << " characters in " << argv[file] << endl;
        total += count;
        fin.clear(); // needed for some implementations
        fin.close(); // disconnect file
    }
    cout << total << " characters in all files\n";

    return 0;
}
```

# Note

Some C++ implementations require using fin.clear() at the end of the program, and others do not. It depends on whether associating a new file with the ifstream object automatically resets the state state. In does no harm to use fin.clear() even if it isn't needed.