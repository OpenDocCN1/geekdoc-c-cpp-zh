
Write a program that reads the file and uses the class to store the countries' data in a vector of Country Elements, the program should read a number and display the data of the countries with higher population than this. Add any function in the class you have needed.

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
#include <vector>
using namespace std;

class Country {
private:
    string name;
    string capital;
    int pop;
public:
    Country(const string& n = "", const string& c = "", int p = 0) : name(n), capital(c), pop(p) {}
    void set(const string& n, const string& c, int p);
    int get_pop() const { return pop; }
    void show() const;
};

void Country::set(const string& n, const string& c, int p) {
    name = n;
    capital = c;
    pop = p;
}

void Country::show() const {
    cout << name << '\t' << capital << '\t' << pop << '\n';
}

int main() {
    int i, pop;
    string name, capital;
    Country tmp;
    vector<Country> cntr;

    ifstream fin("country.txt");
    if(fin.is_open() == false) {
        cout << "Error: is_open() failed\n";
        exit(EXIT_FAILURE);
    }
    while (1) {
        if(!fin >> name >> capital >> pop) {
            break;
        }
        tmp.set(name, capital, pop);
        cntr.push_back(tmp);
    }

    cout << "Enter population: ";
    cin >> pop;
    for(i = 0; i < cntr.size(); i++)
        if(cntr[i].get_pop() >= pop)
            cntr[i].show();

    fin.close();
    return 0;
}
```

# WRITE AND READ DATA FROM A BINARY FILE

The functions used to write and read data/from binary file are the write() and read(), respectively. Although they are primarily used with binary files, they can also be used, with some caution, with text files.

# The write() Function

The write() function is very useful for writing large blocks of data in a single step. Its prototype is:

```cpp
ostream& write(const char *buf, streamsize count);
```

The buf argument points to the memory that holds the data to be written in the file. The streamsize is a synonym for some integer type. The count argument specifies the number of bytes to be written in the file. For example, to store an array of 1000 integers we write:

```cpp
int arr[1000];
ofstream fout("test.dat", ios_base::out | ios_base::trunc | ios_base::binary);
fout.write((char*)arr, sizeof(arr));
```

To store a double number we write:

```cpp
double d = 1.2345;
fout.write((char*)&d, sizeof(double));
```

And to store an object of the Student class we write:

```cpp
Student s;
fout.write((char*)&s, sizeof(s));
```

Note that only the data of the object are written to the file, not the functions. As in the examples, we should cast the address to char*. The best practice is to use the sizeof operator to specify the size, in order to make your program platform independent. And if we want to verify that no error occurred, we check the state of the stream. For example:

```cpp
if(!fout)
    cout << "write error\n";
```

# The read() Function

Like write(), read() is very useful for reading large blocks of data in a single step. Its prototype is:

```cpp
istream& read(char *buf, streamsize count);
```

The buf argument points to the memory in which the read data will be stored. The count argument specifies how many bytes will be read from the file.

> Because two systems differ (e.g., in the size of types), there is no guarantee that a file written with the write() function will be read correctly with the read() function in another system.

In the following example, a double number is read and stored in d:

```cpp
double d;
ifstream fin("test.dat", ios_base::in | ios_base::binary);
fin.read((char*)&d, sizeof(d));
```

In the next example, 1000 integers are read and stored in arr:

```cpp
int arr[1000];
fin.read((char*)arr, sizeof(arr));
```

> It is safer to use write() and read() with binary rather than text files, because potential translations of the new line character can cause unexpected results.

For example, suppose we use write() to write a string of 50 characters in a text file and the value of count is set to 50. If the program runs in Windows and the string contains line character(s), the replacement(s) with the \r\n pair would make its size more than 50; therefore, write() won't write the entire string.

As we will see in the following examples, write() and read() are often used with objects that occupy the same amount of memory. As we said, when we store an object in the file only the data members are stored. However, be careful with classes that use virtual functions. This pointer will change to location, if we run this program to crash. Thus, the pointer will be invalid, if we read the file. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash. The next time we run this, the pointer will change to location, if we run this program to crash.

As we will see in the following examples, write() and read() are often used with objects that occupy the same amount of memory. As we said, when we store an object in the file only the data members are stored. However, be careful with classes that use virtual functions. This pointer will change to location, if we run this program to crash. Thus, the pointer will be invalid, if we read the file. The next time we run this, the pointer will change to location, if we run this program to crash.

# EXERCISES

- **24.8** Write a program that declares an array of 10 integers and writes them in a binary file selected by the user. Then, the program should read the file and display the is is in the.
- **22..** Write a a that that the the size of title, then writes them in a binary file selected by the user. Next, the program should read the file and display the contents.
- **24.9** Write a program that reads the size of title, then writes them in a binary file selected by the user. Next, the program should read the file and display if it is contained in the.

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
#include <cstring>
using namespace std;

int main()
{
    bool found;
    int i, len;
    char title[100], str[100];
    string fname;

    cout << "Enter file name: ";
    cin >> fname;

    fstream fstr(fname.c_str(), ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    if(fstr.is_open() == false) {
        cout << "Error: is_open() failed\n";
        exit(EXIT_FAILURE);
    }
    cin.get();
    for(i = 0; i < 10; i++)
    {
        cout << "Enter title: \";
        cin.getline(title, sizeof(title));
        len = strlen(title);
        fstr.write((char*)&len, sizeof(int));
        fstr.write(title, len);
    }
    cout << "Enter title to search: \";
    cin.getline(str, sizeof(str));

    found = 0;
    fstr.seekg(0);
    while (1)
    {
        if (!fstr.read((char*)&len, sizeof(int)))
            break;
        fstr.read(title, len);
        if (!fstr)
        {
            break;
        }
        title[len] = '\0';
        if(strcmp(title, str) == 0)
        {
            found = 1;
            break;
        }
    }
    if(found == 0)
        cout << "\nTitle not found\n";
    else
        cout << "\nTitle found\n";
    fstr.close();
    return 0;
}
```

24 Files 797

C.24 Suppose that the test.bin binary file contains the grades of a student. The number of grades is declared in the beginning of the file. Write a program that reads the grades from the binary file (using the float type) and stores them in a dynamically allocated memory. Then, the program should read a number and display the grades greater than that number.

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
using namespace std;
```
