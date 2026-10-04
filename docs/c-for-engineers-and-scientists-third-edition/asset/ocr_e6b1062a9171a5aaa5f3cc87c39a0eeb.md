# 716 Structures

# Program 13.3

```
#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

const int NUMRECS = 5;    // maximum number of records

struct PayRec // this is a global declaration
{
    int id;
    string name;
    double rate;
};

int main() {
    int i;
    PayRec employee[NUMRECS] = {
        { 32479, "Abrams, B.", 6.72 },
        { 36623, "Bohm, P.", 7.54 },
        { 34145, "Donaldson, S.", 5.56 },
        { 35987, "Ernst, T.", 5.43 },
        { 36203, "Gwodz, K.", 8.72 }
    };

    cout << endl;    // start on a new line
    cout << setw(ios::left); // left-justify the output
    for ( i = 0; i < NUMRECS; i++) {
        cout << setw(7) << employee[i].id
        cout << setw(15) << employee[i].name
        cout << setw(6) << employee[i].rate << endl;
    }

    return 0;
}
```

Program 13.3 displays the following output:

32479 Abrams, B. | 6.72
36623 Bohm, P. | 7.54
34145 Donaldson, S. | 5.56
35987 Ernst, T. | 5.43
36203 Gwodz, K. | 8.72