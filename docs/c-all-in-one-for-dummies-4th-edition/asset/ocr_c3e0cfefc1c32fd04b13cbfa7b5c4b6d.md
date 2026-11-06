```
}

outfile.close();
return 0;
}
```

![](bbox=[0.172, 0.223, 0.239, 0.291])

By comparing Listing 3-3 with Listing 3-5, and Listing 3-4 with Listing 3-6, you can see that this approach uses fewer lines of code and is somewhat simpler to read. Of course, you don't get the number of records as an immediate output either. Whether the extra coding needed to accommodate the number of records is worthwhile depends on how you use the data. For example, you might need the number of records to create an array to store the data.

# **LISTING 3-6: Reading the Data from Disk Using EOF**

```
#include <iostream>
#include <fstream>
#include <string.h>

using namespace std;

int ReadFile(string filename) {
    ifstream infile(filename);
    if (!infile) {
        cerr << "File couldn't be opened!" << endl;
        cerr << "Error Code: " << strerror(errno) << endl;
        return -1;
    }

    int num;
    cout << "File: " << filename << endl;

do {
    infile >> num;
    cout << num << endl;
} while (!infile.eof());

infile.close();
return 0;
}
```