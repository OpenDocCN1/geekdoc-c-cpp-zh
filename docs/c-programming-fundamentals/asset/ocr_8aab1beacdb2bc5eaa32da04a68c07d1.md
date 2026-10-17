**3. Closing a file:** This is the last, important step in file handling. At program termination, the memory is freed automatically. However, as to not take any chances and risk an item leak, we should always close our files.

# Code: Working with File Operations

```
```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
fstream ourFile;
ourFile.open("OurFile", ios::out);
if(!ourFile)
{
cout<<"File was not created";
}
else
{
cout<<"Our new file has been created";
ourFile.close();
}
return 0;
}
```
```

# Output:

Our new file has been created%

# Code Debriefing

+   - In this code, we used the `fstream` class and created its object.
+   - We used the open method to access our file in open mode.
+   - The program then prints the message “Our new file has been created.”
+   - The `close` method is called upon to close the file we opened earlier.

# Code:Working with Text File

```
```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main()
```
```