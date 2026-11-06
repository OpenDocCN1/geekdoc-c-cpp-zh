# # Manipulating Directories

There are a couple functions you can use for creating and deleting directories. These functions are in the i o . h header file.

# ## Creating a directory

If you want to create a directory, you can call the mkdir function. If the function can create the directory for you, it returns a 0. Otherwise it returns a nonzero value. (When we ran it we got a −1, but your best bet — always — is to test it against 0.)

Here’s some sample code (found in the MakeDirectory example) that uses this function:

```
```cpp
#include <iostream>
#include <stdio.h>
#include <io.h>

using namespace std;

int main()
{
    if (mkdir("../abc") != 0)
    {
        cout << "I'm so sorry. I was not" << endl;
        cout << "able to create your directory" << endl;
        cout << "as you asked of me. I do hope" << endl;
        cout << "you are still able to achieve" << endl;
        cout << "your goals in life. No go away." << endl;
    }
    return 0;
}
```
```

![](bbox=[0.155, 0.634, 0.23, 0.707])

Notice (as usual) that we used a forward slash (/) in the call to mkdir. In Windows, you can use either a forward slash or a backslash. But if you use a backslash, you have to use two of them (as you normally would to get a backslash into a C++ string). For the sake of portability, we recommend always using a forward slash. After you run this example, you should see a new directory named abc added to the /CPB_AUTO/Book/Chapter04 directory on your system.

![](bbox=[0.155, 0.765, 0.23, 0.838])

It would be nice to create an entire directory-tree structure in one fell swoop — doing a call such as mkdir("/abc/def/ghi/jkl") without having any of the abc, def, or ghi directories already existing. But alas, you can’t. The function won’t create a jkl directory unless the /abc/def/ghi directory exists. That means you have to break this call into multiple calls: First create /abc. Then create /abc/def, and so on.

![](bbox=[0.155, 0.882, 0.23, 0.951])

If you do want to make all the directories at once, you can use the system() function, as we describe in “Using the quick-and-dirty method” sidebar, later in this chapter. If you execute system("mkdir \\abc\\def\\ghi\\jkl"), you will be able to make the directory in one fell swoop.