
The difference between the insertion operator and the put() function is that while the former modifies the format of the output with respect to the manipulators set, the latter ignores manipulator settings. Formatted output is dealt with in one of the later sections of this chapter.

## 7.5.2 Text Input

Text input is achieved in C++:

- The extraction operator
- The get() function
- The getline() function

The extraction operator in this chapter, the extraction operator can be used to input values from disk files. The extraction operator inputs in text mode.

The extraction operator has been defined and overloaded in the class istream. It takes an object of the class istream or an object of a class that is derived from the class istream as its left-hand side. As its right-hand side, it takes a variable of one of the fundamental data types. It copies the value found at the current location in the file that is associated with the object on its left into the variable on it. Let us study its action on data of different types. We must keep in mind that the extraction operator has been overloaded differently each of the data types as follows:

1. **Extracting characters from input streams using the extraction operator:** If the right-hand side of the extraction operator is a character-type variable, it reads one byte from the input file that is attached to the object on its left and writes it into the variable (Listing 7.7).

> Listing 7.7 Inputting a character in text mode using the extraction operator

```cpp
/*Beginning of charFileInputText.cpp*/
#include<iostream.h>
#include<fstream.h>
void main() {
    ifstream ifile("first.dat"); //Current location is at
    //the beginning of the file.
    //Suppose first byte in the
    //file contains 'A'.
    char Var;
    ifile>>Var;
    cout<<Var;
}
/*End of charFileInputText.cpp*/
```
Output
A

2. **Extracting integers from input streams using the extraction operator:** If the right-hand side of the extraction operator is an integer-type variable, it reads bytes from the input file that is attached to the object on its left until it finds a white space. It reckons that the read set of bytes represents an integer in base 10 format. Therefore, the extraction operator converts the value into base 2 format. Finally, it writes the converted value into the variable.

Suppose the contents of a file first.dat are as follows:

11 22 33

We must note that there is a space after ‘11’. The first byte of the file has the ASCII equivalent of the character ‘1’. The second byte also has the ASCII equivalent of the character ‘1’. The third byte has the ASCII equivalent of the character ’ (space). The fourth byte has the ASCII equivalent of the character ‘2’ and so on.
Now let us consider Listing 7.8.

# Listing 7.8 Inputting an integer in text mode using the extraction operator

```cpp
/*Beginning of intfileInputText.cpp*/
#include<iostream>
#include<fstream>
void main()
{
    ifstream ifile("first.dat");
    int iVar;
    ifile>>iVar;
}
/*End of intfileInputText.cpp*/
```
Output
11

As discussed, the extraction operator reads from the file until it finds a white space. Since the third byte contains a white space, it reads the first two bytes only. These two bytes represent the number eleven in base 10 format. The extraction operator converts this into base 2. The resulting value is in four bytes. It writes this into the variable ‘iVar'.

3. **Extracting floats and doubles from input streams using the extraction operator:** Values for float and double-type variables are extracted in the same as they are for integer type variables.

4. **Extracting strings from input streams using the extraction operator:** As in the case of integers, the extraction operator reads from the file until it finds a white space while reading value for a character array.

Suppose the contents of a file first.dat are:

abc def ghi

We must note that there is a white space after ‘c’. See Listing 7.9.

# Listing 7.9 Inputting a character array using the extraction operator

```cpp
/*Beginning of charArrayInputText.cpp*/
#include<iostream>
#include<fstream>
void main()
{
    ifstream ifile("first.dat");
    char cArr[20];
    ifile>>cArr;
    cout<<cArr;
}
/*End of charFileInputText.cpp*/
```
Output
abc

Obviously, the extraction operator read up to the white space and stored the read value in the character array.

5. **Extracting objects from input streams using the extraction operator:** If we want to use the extraction operator for extracting objects of a particular class from the input stream, we have to overload it for that. The concept of operator overloading, its need, and its use are elucidated in a later chapter.

## The get() function

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

Suppose the contents of a file first.dat are as follows:

abcd

Listing 7.10 Inputting a character by using the get() function

```cpp
/*Beginning of charFileInputText.cpp*/
#include<iostream.h>
#include<fstream.h>
void main() {
  ifstream ifile("first.dat");
  char cVar;
  ifile.get(cVar);
  cout<<cVar;
}
/*End of charFileInputText.cpp*/
```
Output
a

## The get() function

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

Suppose the contents of a file first.dat are as follows:

abcd

Listing 7.10 Inputting a character by using the get() function

```cpp
/*Beginning of charFileInputText.cpp*/
#include<iostream.h>
#include<fstream.h>
void main() {
  ifstream ifile("first.dat");
  char cVar;
  ifile.get(cVar);
  cout<<cVar;
}
/*End of charFileInputText.cpp*/
```
Output
a

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined has the defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined has the the defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined has the defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined in the class istream. It reads one byte from the input file and stores it in the character variable that is passed as a parameter to it (Listing 7.10). The prototype of the get() function is as follows:

istream & :: get(char &);

The get() function has been defined has the defined in the class istream. (Wait, this is repeating).

## 7.6 Binary Output—Function

## 7.6.1 Binary Output—Function

The write() function copies the values of variables from memory to the specified output file. It works in binary mode. As we know, binary functions are not concerned about the data type of the variable that is output. They are only interested in the address of the variable (starting point of the block whose data needs to be output) and the size of the variable (total number of bytes to output). The prototype of the write() function makes this clear:

```cpp
ostream & write(const char *, int);
```

The write() function has been defined in the class ostream. It takes two parameters. The first parameter is the address of the variable whose value needs to be output. The second parameter is the size of the variable. The write() function writes the value of the variable to the file that is associated with the object with which it has been called.
Let us now discuss how the write() function is used to output data of various types.

1. **Inserting characters into output streams using write() function:** Listing 7.13 illustrates how the write() function can be used to output the value of a character-type variable to a disk file.

# Listing 7.13 Using the write() function to output character-type value to a disk file

```cpp
/*Beginning of writeCharDisk.cpp*/
#include<fstream.h>
void main() {
  ofstream ofile("first.dat");
  char cVar;
  cVar = 'a';
  ofile.write(cVar,sizeof(char));
}
/*Beginning of writeCharDisk.cpp*/
```
