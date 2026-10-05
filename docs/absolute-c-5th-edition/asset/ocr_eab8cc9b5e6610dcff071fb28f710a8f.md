# Display 12.2 Appending to a File

```
// //Appends data to the end of the file aldata.txt.
#include <fstream>
#include <iostream>
using std::ofstream;
using std::cout;
using std::ios;

int main() 
{
    cout << "Opening data.txt for appending.\n";
    ofstream fout;
    fout.open("data.txt", ios::app);\n    fout << "5 6 pick up sticks.\n";
    fout << "7 8 ain't C++ great!\n";
    cout << "End of appending to file.\n";
    return 0;
}
```

Sample Dialogue

# Data.txt
(Before program is run)

# Data.txt
(After program is run)

| 1 buckle my shoe. |
| 3 shut the door. |

| 1 2 buckle my shoe. |
| 3 shut the door. |
| 5 6 pick up sticks. |
| 7 8 ain't C++ great! |

# Screen Output

![](bbox=[0.315, 0.732, 0.665, 0.792])