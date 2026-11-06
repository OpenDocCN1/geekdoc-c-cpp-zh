![](bbox=[0.159, 0.091, 0.218, 0.152])

If you try to open a file for writing by specifying a full path and filename but the directory does not exist, the computer responds differently, depending on the operating system you're using. If you're unsure how your particular operating system will respond, try writing a simple test application that tries to create and open a nonexistent path like /abc/def/ghi/jkl/abc.txt. Then one of the following will happen:

+   - The operating system will generate an error (the default for Windows).
+   - The operating system will create the required path and file.

If you want to determine whether the ostream class was unable to create a file, you can call its fail() method. This method returns true if the object couldn't create the file. That's what happens when a directory doesn't exist. The DirectoryCheck01 example, shown in Listing 1-5, demonstrates an example of using the fail() method.

# LISTING 1-5: Returning True When ostream Cannot Create a File

```
```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
    ofstream outfile("/abc/def/ghi/MyFile.txt");
    if (outfile.fail()) {
        cout << "Couldn't open the file!" << endl;
        return 0;
    }
    outfile << "Hi" << endl;
    outfile.close();
    return 0;
}
```
```

When you run this code, you should see the message Couldn't open the file! when your particular operating system doesn't create a directory. If it does, your computer will open the file and write Hi to it.

As an alternative to calling the fail() method, you can use an operator available in various stream classes. This is !, fondly referred to as the bang operator, and you would use it in place of calling fail(), as in this code:

```
```
if (!outfile)
{
```
```