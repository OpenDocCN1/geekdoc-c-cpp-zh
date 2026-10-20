# File Input/Output

The standard iostream library provides C++ coders with the cin and cout input and output functionality. However, to be able to read and write from a file you need to utilise another C++ library, called fstream.

# FSTREAMS

There are two main data types within the fstream library that are used to open a file, read from it and write to it, ofstream and ifstream. Here's how they work.

# STEP 1

The first task is to create a new C++ File and along with the usual headers you need to include the new fstream header:

```
#include <iostream>
#include <fstream>
Using namespace std;

int main ()
{
```

![](bbox=[0.07, 0.54, 0.49, 0.66])

# STEP 2

Begin by asking a user for their name and writing that information to a file. You need the usual string to store the name, and getline to accept the input from the user.

```
#include <iostream>
#include <fstream>
using namespace std;

int main ()
{
    string name;
    ofstream newfile;
    newfile.open("name.txt");
    cout << "Enter your name: " << endl;
    getline(cin, name);
    newfile << name << endl;
    newfile.close();
}
```

# STEP 3

We've included comments in the screenshot of step 2 to help you understand the process. You created a string called name, to store the user's inputted name. You also created a text file called name.txt (with the ofstream newfile and newfile.open lines), asked the user for their name and stored it and then written the data to the file.

![](bbox=[0.52, 0.46, 0.93, 0.58])

# STEP 4

To read the contents of a file, and output it to the screen, you need to do things slightly differently. First you need to create a string variable to store the file's contents (line by line), then open the file, use getline to read the file line by line and output those lines to the screen. Finally, close the file.

```
string line;
ifstream newfile ("name.txt");

cout << "Contents of the file: " << endl;

getline(newfile, line);
cout << line << endl;
newfile.close();
```

![](bbox=[0.52, 0.78, 0.93, 0.94])