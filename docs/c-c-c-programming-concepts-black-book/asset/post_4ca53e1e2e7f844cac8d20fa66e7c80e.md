
The << operator is called the *inserter*, and *cout* is an object of type *ostream* defined in the *iostream* header file and is attached to the standard output device. The preceding statement signifies that the text string to the right of the inserter is to be stored in the stream object to the left. The << operator accepts a string or char * as an argument. It also accepts all the fundamental data types as arguments.

## Stream Insertions and Extraction

In the C++ language, the << output operator is referred to as the insertion operator because it inserts the characters into a stream. Likewise, the >> input operator is known as the extraction operator, as it extracts the characters from the stream. The features that overload the insertion and extraction operators are called inserters and extractors, respectively.

The generic format of an inserter is as follows:

```cpp
ostream&operator<<(ostream &stream, classType obj)
{
    ....
    return stream;
}
```

In the preceding format, note that the function returns a reference of the stream associated with the type ostream, which is a class based on ios that facilitates output. The first parameter to the function is a reference to the output stream. The second parameter may be an object or a reference towards an object that is inserted. Finally, the inserter exits by returning the stream. This enables the inserter to be used in a bigger I/O expression.

Inside an inserter function, we can put any kind of procedures. However, we should limit its operations to outputting information to some stream.

The opposite of insertion is extraction, which refers to the fetching of data from an input stream. Input stream operations are defined in the *istream* class. The overloaded operator >> (right shift bitwise operator) is called an *extractor*, and it is overloaded to accept three data types: integers, floating points, and characters.

The general form of an extractor is as follows:

```cpp
istream&operator>>(istream &stream, classType &obj)
{
    ....
    return stream;
}
```

Extractors return a reference to a stream of type istream, and it is an input stream. The first parameter needs to be a reference to a stream of type istream. Note that the second parameter has to be a reference to an object of the class.

### Integer and Floating-Point Extraction

*cin* is an object of type istream and is defined in the *iostream* header file. It is associated with the standard input device, that is, the keyboard. Now, consider the following statements:

```cpp
int i;
cin>> i;
```

If the input from a user through the keyboard is <space><space>375g54, then *i* will contain 375. The input buffer will contain g54, and the pointer will be positioned at g. This is because integer extraction bypasses the whitespaces and reads the input characters until it encounters a character that cannot be a part of that data type.

Now, consider the following statements:

```cpp
float f;
cin>> f;
```

If the input from a user through the keyboard is −527e-35d8, then −527e-35 will be fetched into f and the input pointer will be positioned at d. This is because floating-point extraction bypasses the whitespaces and reads the input characters until a non-floating-point character is encountered.

### Character Extraction

The character extractor does not work the way one might expect. It reads the next character in the stream after skipping the whitespaces. For example, if we enter <space>X, then the extractor would ignore the whitespace and return X. Therefore, char * (or string) extractors often yield unpredictable results. Consider the following statements:

```cpp
char str1[25], str2[25];
cin>> str1;
cin>> str2;
```

If a user enters <space>Thomas<space>Vienna<return>, then str1 will contain Thomas and str2 will contain Vienna. This is because character extraction terminates the moment a whitespace is encountered.

### Implicit File Opening and Closing

In C++, a file can be opened or closed without using any open or close function. To open a file, the name of file can be passed as an argument to a constructor, shown as follows:

```cpp
ofstream ob("student.dat");
```

In the preceding statement, ob is an object of the ofstream class whose constructor is responsible to open a student.dat file. Similarly, destructor of the ofstream class is responsible to close a file. When we open a file implicitly by using the ofstream class, the file will be opened in the write mode by default. Similarly, the file will be opened in the read mode when we open it implicitly by using the ifstream class.

### Extraction and Insertion of Fundamental Data Types

Let’s learn about file I/O using fundamental data types. Consider the following code to write some integers to a file:

```cpp
#include<iostream>
using namespace std;
void main()
{
    ofstream OP("INTEGER.TXT");
    OP<< 25 <<' '<< 1234 <<' '<< 5678;
}
```

In the preceding code, we have created an object OP of the ofstream class and associated it with a file, named INTEGER.TXT. We have used the << stream insertion operator to write data into OP. The INTEGER.TXT file can be typed and checked for its contents.

To read the data back from a file, we need to write the following block of code:

```cpp
#include<iostream>
using namespace std;
void main()
{
    ifstream IP("INTEGER.TXT");
    int i, j, k;
    IP >> i >> j >> k;
    cout<< i << ' ' << j << ' ' << k;
}
```

The reason for using space during insertion is that in case of any stream extraction, the integer extractor reads all the characters up to the first character, which is not of integer data type. For this, first consider the following code:

```cpp
#include<fstream.h>
void main()
{
    ofstream OP("STRING.DAT");
    OP << "Hello World";
}
```

Now, consider the following code:

```cpp
#include<fstream.h>
void main()
{
    ifstream IP("STRING.DAT");
    char str[30];
    IP >>str;
    cout<< str;
}
```

The output of the preceding program is Hello, as the character extraction does not recognize whitespaces. This implies that the problem of character stream extraction also exists during file I/O.

## File I/O Using Objects

Objects can also be used in a program to perform file I/O operations. Consider the following code:

```cpp
#include<iostream.h>
#include<fstream.h>
#include<conio.h>
using namespace std;
int main()
{
    ofstream outf("d:/CPP/TEST.txt");
    if(!outf.good()==0 )
    {
        cout<<"Error opening the file.......";
        getch();
        return 0;
    }
    char name[30];
    cout<<"Enter your name...";
    cin>>name;
    outf<<name<<"\n";

    int age;
    cout<<"Enter your age....";
    cin>>age;
    outf<<age<<"\n";
    outf.close();

    ifstream inf("d:/CPP/TEST.txt ");
    if(!inf.good()==0 )
    {
        cout<<"Error opening the file.......";
```

- **istream& get (streambuf& sb)** – It extracts the characters with a stream and inserts all of them inside the stream buffer sb till either the delimiting character '\n' is available or the end associated with the statement occurs. The extraction also stops if an error occurs inside the input sequence controlled by using the stream or inside the output sequence controlled by using sb.
- **istream& get (streambuf& sb, char delim)** – It is identical as above, except how the delimiting character may be the one specified in delim rather than '\n'.

The put() function is used to write in a file. Consider the following code to understand the use of the put() function:

```cpp
#include<fstream>
#include<string.h>
using namespace std;
void main()
{
    ofstream outfile("d:/EXAMPLE.TXT");
    char str[] = "This is a simple example";
    for(int i = 0; i<strlen(str); i++)
        outfile.put(str[i]);
        outfile.put('\0');
}
```

The preceding code when executed will create a file EXAMPLE.txt in the D directory. The content of the EXAMPLE.txt file is “This is a simple example”.

Now, consider the following code:

```cpp
#include<iostream.h>
using namespace std;
void main()
{
    char str[20];
    cin.get(str,20);
    cout<<str;
}
```

The preceding code gets a string along with the whitespaces from the console input and displays the string on the standard output. Another function that can be used for string input is:

```cpp
getline(char * s, int len, char delim = '\n');
```

The getline() function is similar to the get() function, but it extracts the terminator as well. Let’s make the changes in the preceding program using the getline() function as follows:

```cpp
#include<iostream.h>
using namespace std;
void main()
{
    char str[20];
    cin.getline(str,20);
    cout<<str;
}
```

The only difference between the previous program and this one is that str will also contain the '\n' character.

## The read() and write() Functions

The read() function is called with two arguments – the address of the buffer into which the file is to be written and the size of the buffer. The write() function also requires similar arguments. Consider the following code snippet to read a series of values from a user and write it to a file:
