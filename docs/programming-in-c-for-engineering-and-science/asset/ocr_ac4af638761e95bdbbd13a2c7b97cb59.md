Input: a series of values from a file
Output: each value and its difference from the average value

```
#include <iostream>    // cout, <<, >>
#include <fstream>    // ifstream, is_open(), eof(), clear(), seekg()
#include <iomanip>
#include <string>
#include <cassert>    // assert
using namespace std;

int main()
{
    string inputFileName;
    cout << "Name of data file? ";
    cin >> inputFileName;
    ifstream inStream(inputFileName.data());
    assert(inStream.is_open());

    double newValue, sum = 0.0, average = 0.0;
    int count = 0;

    for (;;)
    {
        inStream >> newValue;
        if (inStream.eof()) break;
        sum += newValue;
        count++;
    }

    if (count > 0) average = sum / count;

    inStream.clear();    // clear eof bit
    inStream.seekg(0, ios::beg); // reset read position

    cout << endl;

    for (;;)
    {
        inStream >> newValue;
        if (inStream.eof()) break;
        cout << setw(10) << newValue << " : "
             << setw(10) << newValue - average << endl;
    }
    inStream.close();
}
```

# SAMPLE RUN:

Name of data file? test1.txt

11.1 :     -44.4
22.2 :     -33.3