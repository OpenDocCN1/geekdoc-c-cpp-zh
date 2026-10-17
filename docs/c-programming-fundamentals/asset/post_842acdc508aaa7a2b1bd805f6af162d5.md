
- a. Exception received  
- b. Divide by zero  
- c. Syntax error  
- d. No output  

- 48. What is the correct output of the given code snippets?

```cpp
#include <iostream>
using namespace std;
int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;

        if (B == 0) {
            exception E;
            throw E;
        }
        C = A / B;
    }
    catch (exception E) {
        cout << "Exception Received" << endl;
    }
    return 0;
}
```

- a. Exception Received  
- b. Divide by zero  
- c. Syntax error  
- d. No output  

- 49. What is the correct output of the given code snippets?

```cpp
#include <iostream>
using namespace std;

int main()
{
    try {
        int A = 10;
return 0;
}
```

- a. ###Exception Received  
- b. @@@Exception Received  
- c. Syntax error  
- d. No output  

- 51. What is the correct output of the given code?

```cpp
#include <iostream>
using namespace std;

int main()
{
    try {
        int A = 10;
        int B = 0;
        int C;
        if (B == 0) {
            bad_exception E;
            throw E;
        }
        C = A / B;
    }
    catch (bad_exception E) {
        cout << "@@@Exception Received" << endl;
    }
    catch (exception E) {
        cout << "###Exception Received" << endl;
    }
    return 0;
}
```

- a. ###Exception Received  
- b. @@@Exception Received  
- c. Syntax error  
- d. No output  

## MCQ

| 1. (a) | 2. (b) | 3. (a) | 4. (a) | 5. (b) | 6. (a) | 7. (d) | 8. (a) | 9. (b) | 10. (c) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 11. (d) | 12. (c) | 13. (d) | 14. (c) | 15. (c) | 16. (c) | 17. (b) | 18. (b) | 19. (c) | 20. (d) |
| 21. (d) | 22. (b) | 23. (c) | 24. (c) | 25. (c) | 26. (d) | 27. (a) | 28. (a) | 29. (b) | 30. (a) |
| 31. (b) | 32. (a) | 33. (b) | 34. (a) | 35. (a) | 36. (c) | 37. (b) | 38. (d) | 39. (a) | 40. (a) |
| 41. (b) | 42. (a) | 43. (d) | 44. (d) | 45. (a) | 46. (a) | 47. (c) | 48. (a) | 49. (a) | 50. (a) |
| 51. (b) |  |  |  |  |  |  |  |  |  |

## References

### Books

- B. Stroustrup, *The C++ Programming Language* (4th Edition) (Addison-Wesley Professional, 2013).
- K. R. Venugopal, *Mastering C++* (2nd Edition) (McGraw Hill Education, July 2017).
- Y. Kanetkar, *Let Us C++* (BPB Publications September, 2020).
- Y. Kanetkar, *Test Your C++ Skills* (BPB Publications March, 2003).

### Websites

- Learn CPP, accessed August 2022, *https://www.learncpp.com*
- Codes Cracker, accessed August 2022, *https://codescracker.com*
- Roll Bar, accessed August 2022, *https://rollbar.com*
- Geeks For Geeks, accessed August 2022, *https://www.geeksforgeeks.org*
- Udacity, accessed August 2022, *https://www.udacity.com*
- Scaler, accessed August 2022, *https://www.scaler.com*
- C Plus Plus, accessed August 2022, *https://cplusplus.com*
- Silly Codes, accessed August 2022, *https://sillycodes.com*

## CHAPTER 11 FILE HANDLING

### 11.1 Files and Streams

Organizing and maintaining our belongings helps us access them whenever they are needed with ease, and the same is true for our desktop folders and phone data. All need organizing and efficient handling. In C++, we handle and organize files, folders, and directories. We can write our own files and display the items in created files. What exactly is a file in C++? Let us try to define it in simple terms.

### Files

Files created in C++ help to store data onto the hard disk and remain in the system for later use. This is different from traditional programs, where our data or objects holding data get deleted after program termination to reclaim the temporary memory space allotted. Many times, we need our data to be securely stored in the system so fetching items out of a file requires less time.

### Streams

For the user to enter and provide details or values, we use input streams. A stream refers to a group of bytes that can be accessed sequentially. There are two different types of streams. *Input streams* are used to hold the input from a user, such as a keyboard. For example, the user might press any key on the keyboard, even when not asked for it. In a situation like

### Code: Working with Files and Streams

```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
    ofstream ofObj;
    string ourLine;
    ofObj.open("textFile3.txt");
    while (ofObj)
    {
        getline(cin, ourLine);
        if (ourLine == "-1")
            break;
        cout << ourLine << endl;
    }
    ofObj.close();
    ifstream ifObj;
    ifObj.open("textFile3.txt");
    while (ifObj)
    {
        getline(ifObj, ourLine);
        cout << ourLine << endl;
    }
    ifObj.close();
    return 0;
}
```

**Output:**

```text
We are learning and improving everyday.
We are learning and improving everyday.

-1
```

### Code Debriefing

- In this code, we used the `ofstream` class and created its object and a string value.
- We then used the `open` method to access our file in open mode.
- Text entered is written onto the file using the `ifstream` class object.
- The program then prints the content of the newly written file.
- The `close` method is called upon to close the file we had opened earlier.

### 11.2 File Operations

The major steps needed in C++ for file handling are as follows:

**Opening a file:** This is the first step taken toward file management in C++ and can be done either by passing our file name in the constructor when an object is created or using the `open()` method.

The syntax for opening a file is as follows:

```text
void open(const char* ourFileName, ios::openMode mode);
or
open() function
```

Now, various open modes can be activated in C++.

**Table 11.1** Types of Open Modes

| Serial Number | Mode | What it does |
| --- | --- | --- |
| 1 | `in` | This mode is the default while using `ifstream`, and it opens our file to read. |
| 2 | `out` | This mode is the default while using `ofstream`, and it opens our file to write. |
| 3 | `ate` | This mode opens our file, and the pointer faces the end of the file. |
| 4 | `binary` | This mode opens our file in binary form. |
| 5 | `noreplace` | This mode will open a file only if it does not exist in the system. |
| 6 | `nocreate` | This mode will open a file only if it exists in the system. |
| 7 | `trunc` | This mode will open a file if it already exists, and the items will be truncated. |
| 8 | `app` | This mode will open our file in append mode, and all new items will be appended at the end of the file. |

We can also combine different opening modes by separating each by using the symbol `|`, called the logical or symbol.

- **Writing to a file:** Done using the `ofstream` or `fstream` classes to enter data onto our created or opened files.
- **Reading a file:** Done using the `ifstream` or `fstream` classes to fetch data from our created or opened files.
- **Closing a file:** This is the last, important step in file handling. At program termination, the memory is freed automatically. However, as to not take any chances and risk an item leak, we should always close our files.

### Code: Working with File Operations

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

**Output:**

```text
Our new file has been created
```

### Code Debriefing

- In this code, we used the `fstream` class and created its object.
- We used the `open` method to access our file in open mode.
- The program then prints the message “Our new file has been created.”
- The `close` method is called upon to close the file we opened earlier.

### Code: Working with Text File

```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
    ofstream ofObj;
    string ourLine;
    ofObj.open("textFile3.txt");
    while (ofObj)
    {
        getline(cin, ourLine);
        if (ourLine == "-1")
            break;
        cout << ourLine << endl;
    }
    ofObj.close();
    ifstream ifObj;
    ifObj.open("textFile3.txt");
    while (ifObj)
    {
        getline(ifObj, ourLine);
        cout << ourLine << endl;
    }
    ifObj.close();
    return 0;
}
```

**Output:**

```text
We are learning and improving everyday.
We are learning and improving everyday.

-1
```

### Code Debriefing

- In this code, we used the `ofstream` class and created its object and a string value.
- We then used the `open` method to access our file in open mode.
- Text entered is written onto the file using the `ifstream` class object.
- The program then prints the content of the newly written file.
- The `close` method is called upon to close the file we had opened earlier.
