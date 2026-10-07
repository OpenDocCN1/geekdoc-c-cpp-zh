
## Chapter 17 Input, Output, and Files

between a stream and a file. The class constructors and the open() method take an optional second argument that provides the file mode. The file mode determines such things as whether the file is to be read and/or written to, whether opening a file for writing truncates it, whether attempting to open a non-existent file is an error, and whether to use binary or text mode.

A text file stores all information in character form. For example, numeric values are converted to character representations. The usual insertion and extraction operators, along with get() and getline(), support this mode. A binary file stores all information by using the same binary internally. Binary files store data, particularly floating-point values, more accurately and compactly than text files, but are less portable. The read() and write() methods support binary input and output.

The seekg() and seekp() functions provide C++ random access for files. These methods let you position a file pointer relative to the beginning of a file, relative to the end, or to the current position. The tellg() and tellp() methods report the current position.

The sstream header defines istream and ostream classes that you use stream and ostream methods to extract information from a string and to format information placed into a string.

## Chapter Review

- 1. What role does the iostream file play in C++ I/O?
- 2. Why does typing a number such as 121 as input require a program to make a version?
- 3. What's the difference between the standard output and the standard error?
- 4. Why is cout able to display various C++ types without being explicit instructions for each type?
- 5. What feature of the output method definitions allows you to concatenate output?
- 6. Write a program that requests an integer and displays it in decimal, octal, and hexadecimal forms. Display each form on the same line, in fields that are 15 characters wide, and use the C++ number prefixes.

- 7. Write a program that requests the following information and formats it as shown:
Enter your name: Billy Gruff
Enter your hourly wages: 12
Enter number of hours worked: 7.5
First format: Billy Gruff: $ 12.00: 7.5

Second format:
Billy Gruff : $12.00 :7.5

8. Consider the following program:

```
//rqi17-8.cpp
#include <iostream>

int main() {
    using namespace std;
    char ch;
    int ctl = 0;

    cin >> ch;
    while (ch != 'q') {
        ctl++;
        cin >> ch;
    }

    int ct2 = 0;
    cin.get(ch);
    while (ch != 'q') {
        ct2++;
        cin.get(ch);
    }

    cout << "ctl1" << " = " << ctl << " " << "ct2" << " = " << ct2 << "\n";

    return 0;
}
```

What does it print, given the following input:

I see a q-Enter
I see a q-Enter

Here <Enter> signifies pressing the Enter key.

9. Both of the following statements read and discard characters up to and including the end of a line. In what way does the behavior of one differ from that of the other?

```
while (cin.get() != '\n')
    continue;
cin.ignore(80, '\n');
```

## Programming Exercises

- 1. Write a program that counts the number of characters up to the first $ in input and that leaves the $ in the input stream.

- 2. Write a program that copies your keyboard input (up to the simulated end-of-file) to a file named on the command line.

- 3. Write a program that copies one file to another. Have the program take the file-names from the command line. Have the program report if it cannot open a file.

- 4. Write a program that opens two text files for input and for output. The program should contains the corresponding lines of the input files, use a space as a separator, and writes the results to the output file. If one file is shorter than the remaining lines in the longer file should also be copied to the output file. For example, suppose the first input file has these contents:
```
egs kites donuts
balloons hammers

```
And suppose the second input file has these contents:
```
z lassitude
finance drama
```
The resulting file would have these contents:
```
egs kites donuts zero lassitude
balloons hammers finance drama

```

- 5. Mat and Pat want to invite their friends to a party, much as they did in Programming Exercise 8 in Chapter 16, except now they want a program that uses files. They have asked you to write a program that does the following:

- Reads a list of Mat's friends' names from a text file called mat.dat, which lists one friend per line. The names are stored in a container and then displayed in sorted order.
- Reads a list of Pat's friends' names from a text file called pat.dat, which lists one friend per line. The names are stored in a container and then displayed in sorted order.
- Merges the two lists, eliminating duplicates and stores the result in the file matpat.dat, one friend per line.

## Programming Exercises

- 6. Consider the class definitions of Programming Exercise 5 in Chapter 14, "Reusing Code in C++". If you haven't yet done that exercise, do so now. Then do the following:

Write a program that uses standard C++ I/O and file I/O in conjunction with types employee, manager, fink, and highfrank, as defined in Programming Exercise 5 in Chapter 14. The program should follow the general lines of Listing 17.17 in it that you should add new data to a file. The first time, the program should solicit data from the user, show all the entries, and save the information in a file. On subsequent uses, the program should first read and display the file data, the user add data, and show all the data. One difference is that data should be handled by an array of pointers to type employee. That way, a pointer can point to an employee object or to any of the three derived types. Keep the array small to facilitate the array to 10 elements:

```
const int MAX = 10; // no more than 10 objects
...
employee * pc [MAX];
```

For keyboard entry, the program should use a menu to offer the user the choice of which type of object to create. The menu should use a switch to create an object of the desired type and to assign the object's address to a pointer in the pc array. Then that object can use the virtual setall() function to elicit the appropriate data from the user:

```
pc[i]->setall(); // invokes function corresponding to type of object
```

To save the data to a file, devise a writeall() function for that purpose:
for (int i = 0; i < index; i++)
pc[i]->writeall(fout); // fout stream connected to output file

> Note
Use I/O, not binary I/O, for Programming Exercise 6. (Unfortunately, virtual objects includes pointers to tables of virtual functions, and write() copies this information to a file. An object filled by using read() from the file gets values for the function pointers, which really means the behavior of virtual functions.) A newline character to separate each data field from the next; this makes it easier to identify fields on input. Or you could still use binary I/O, but not write objects as a whole. Instead, you could provide class methods that apply the write() and read() functions to each class individually rather than to the object as a whole. That way, the program could save just the intended data to a file.

## Chapter 17 Input, Output, and Files

The tricky part is recovering the data from the file. The problem is, how can the program know whether the next item to be recovered is an employee object, a manager object, a fink type, or a highfink type? One approach is, when writing the data for an object to a file, precede the data with an integer that indicates the type of object to follow. Then, on input, the program can read the integer and then use switch to create the appropriate object to receive the data:

```
enum kind<Employee, Manager, Fink, Highfink>; // in class header
...
int classtype;
while((fin >> classtype).get(ch)) { // newline separates int from data
switch(classtype) {
  case Employee : pc[i] = new employee;
    : break;
```

You can use the pointer to invoke a virtual get() function to read the information:

```
pc[i++]->getall();
```

- 7. Here is part of a program that reads keyboard input into a vector of string objects, stores the string contents (not the objects) in a file, and copies the file contents back into a vector of string objects:

```
int main()
{
  using namespace std;
  vector<string> vostr;
  string temp;

  // acquire strings
  cout << "Enter strings (empty line to quit):\n";
  while(getline(cin, temp) && temp[0] != '\0')
    vostr.push_back(temp);
  cout << "Here is your input.\n";
  for_each(vostr.begin(), vostr.end(), ShowStr);

  // store in a file
  ofstream fout("strings.dat", ios_base::out | ios_base::binary);
  for_each(vostr.begin(), vostr.end(), Store(fout));
  fout.close();

  // recover file contents
  vector<string> vistr;
  ifstream fin("strings.dat", ios_base::in | ios_base::binary);
  if (!fin.is_open())
    cerr << "Could not open file for input.\n";
n}
```
