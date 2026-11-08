+   11. To use the function `putback`, the program must include the header file `iomanip`.
+       To use the function `peek`, the program must include the header file `iostream`.

+   13. `getline(cin, name);`

+   15.
+       a. `name = "Lance Grant", age = 23`
+       b. `name = "", age = 23`

+   17.

```
```cpp
#include <iostream>
#include <fstream>

using namespace std;

int main()
{
    int num1, num2;
    ifstream infile;
    ofstream outfile;

    infile.open("input.dat");
    outfile.open("output.dat");

    infile >> num1 >> num2;
    outfile << "Sum = " << num1 + num2 << endl;

    infile.close();
    outfile.close();

    return 0;
}
```
```

+   19. `fstream`

+   21.
+       a. Same as before.
+       b. The file contains the output produced by the program.
+       c. The file contains the output produced by the program. The old contents are erased.
+       d. The program would prepare the file and store the output in the file.

+   23.
+       a. `outfile.open("travel.dat");`
+       b. `outfile << fixed << showpoint << setprecision(2);`
+       c. `outfile << day << " " << distance << " " << speed << endl;`
+       d. `travelTime = distance / speed;`
+          `outfile << travelTime;`
+       e. `fstream` and `iomanip`.