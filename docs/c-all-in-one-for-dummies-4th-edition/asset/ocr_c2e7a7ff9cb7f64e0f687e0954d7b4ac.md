```
```cpp
    if (DataFile.is_open()) {
        DataFile << Text << endl;
    } else {
        cerr << "Unable to open file." << endl;
        return -1;
    }

    DataFile.close();
    return 0;
}
```
```

# **LISTING 3-9: Reading the Complex Data**

```
```cpp
#include <iostream>
#include <fstream>
#include <string.h>

using namespace std;

int ReadData(string Filename) {
    ifstream DataFile(Filename);
    if (!DataFile) {
        cerr << "File couldn't be opened!" << endl;
        cerr << "Error Code: " << strerror(errno) << endl;
        return -1;
    }

    string Data = "";
    while (getline(DataFile, Data)) {
        cout << Data << endl;
    }

    DataFile.close();
    return 0;
}
```
```

Many of the techniques you see in these code listings also appear in the previous examples of this chapter. However, instead of treating the data as separate elements, this example works with strings. This difference in data complexity requires a few changes.

Because the WriteData() function writes data and closes the file each time, appending the new data to the end of the file (using ios_base::app), you need a

Reading with Input Streams