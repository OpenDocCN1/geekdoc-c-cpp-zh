# Program 16.6  Reading from an existing file

```
```cpp
/******************************************************
 * A program to read from an existing file and display data on
 * the monitor                                           *
 ******************************************************/
#include <iostream>
#include <fstream>
#include <cassert>
using namespace std;

int main()
{
    int data;
    // Instantiation of an ifstream object
    ifstream inStrm;
    // Connection of the existing file to the ifstream object
    inStrm.open("IntegerFile");
    if (!inStrm.is_open())
    {
        cout << "integerFile cannot be opened!";
        assert(false);
    }
    // Reading from the ifstream object and writing to the cout object
    for (int i = 1; i <= 10; i++)
    {
        inStrm >> data;
        cout << data << " ";
    }
    // Disconnection of the IntegerFile from the ifstream
    inStrm.close();
    // Destruction of the ifstream object is done after return
    return 0;
}
```

**Run:**

`10 20 30 40 50 60 70 80 90 100`
```

Note that this time we can see the integers printed on the monitor. We read from the *integerFile* using the extraction operator. This operator skips whitespace and reads the data. After each read, we write the data to the cout object (monitor).

# 16.3.2 Opening Modes

In Programs 16.5 and 16.6, we ignored the *opening modes*. We used the default opening mode for the *integerFile* in both cases (when connected to the *ofstream* and when connected to the *ifstream*). The opening mode is a type defined in the *ios* class and inherited by all classes in the hierarchy of stream classes. Opening modes are not used in the console streams or string streams because we do not open them; they are used only in the file