
# Chapter 8 461

Reading and Writing Character-Based Files

# Program 8.6

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib> // needed for exit()
#include <string>
using namespace std;

int main() {
    string filename = "prices.dat"; // put the filename up front
    string line;
    ifstream infile;

    infile.open(filename.c_str());

    if (infile.fail()) // check for successful open
    {
        cout << "\nThe file was not successfully opened"
             << "\nn Please check that the file currently exists."
             << endl;
        exit(1);
    }

    // read and display the file's contents
    while (getline(infile, line)) {
        cout << line << endl;
    }

    infile.close();

    return 0;
}
```

# Standard Device Files

The file streams you have seen so far have been logical file objects. A logical file object is a stream that connects to logically related data, such as a data file, to a program. In addition to logical files, C++ supports physical file objects. A physical file object is a stream that connects to a hardware device, such as a keyboard, screen, or printer.

The actual device assigned to the program for data entry is called the standard input file. Usually, it's the keyboard. When a cin method call is encountered in a C++ program, it is a request to the OS to go to this standard input for expected input. Similarly, when a cout method call is encountered, the output is automatically displayed or "written to" a device that has been assigned as the standard output. For most systems, it's the screen.

# get() and putback() Methods

All input streams have access to the istream class's get() method, used for character-by-character input. This method works similarly to character-extraction using the >> operator, with two important differences: If a newline character '\n', or a blank character ' ', is encountered, these characters are read in the same manner as any alphanumeric character. The syntax of this method call is the following:

```cpp
istream.get(characterVariable);
```

For example, the following code can be used to read the next character from the standard input stream and store it in the variable:

```cpp
char ch;
cin.get(ch);
```

Similarly, if inputFile is an ifstream object that has been opened to a file, the following code reads the next character in the stream and assigns it to the variable:

```cpp
char keycode;
inFile.get(keycode);
```

In addition to the get() method, all input streams have a putback() method for putting the last character read back on the stream. This method has the following syntax (with characterExpression) representing any character or value:

```cpp
inputStream.putback(characterExpression);
```

The putback() method provides output capability to an input stream. The putback character need not be the last character read; it can be any character. All putback characters, however, have no effect on the data file. Therefore, the data remains unchanged although the characters subsequently read from the input stream can change.

When a program is executed, the standard input stream cin is connected to the standard input device. Similarly, two object streams are available for programmer use, as the standard error stream cerr, and the standard log stream clog. These streams connect to the screen.

# Other Devices

The keyboard, display, error, and log streams are connected automatically to the stream objects cin, cerr, and clog the iostream header is included in a program. Other devices can be used for input or output if the name assigned by the system is known. For example, most IBM compatible PCs assign the name lprn to the printer connected to the computer. For these computers, a statement such as outFile.open("prn") connects the printer to the ofstream object named outFile. A subsequent statement, such as outFile << "Hello World!"; would cause the string Hello World! to be output directly to the printer. As the name of an actual file, lprn must be enclosed in quotation marks in the open() method.

![](img/e2a84fc7bc04aa2e669ad865e0c22b_482_0.png)

# EXERCISES 8.2

1. (Practice and Modify) a. Enter and execute Program 8.5. b. Modify Program 8.6 to use the expression !inFile.eof() in place of the expression inFile.good(), and execute the program to see whether it operates.

2. (Practice and Modify) a. Enter and execute Program 8.6. b. Modify Program 8.6 by replacing cout with cerr, and verify that the output for the standard error stream is the screen. c. Modify Program 8.6 by replacing cout with clog, and verify that the output for the standard log stream is the screen.

3. (Practice and Modify) a. Create a C++ program that accepts lines of text the keyboard and writes each line to a file named text.dat until an empty line is entered. An empty line is a line with no text that's created by pressing the Enter (or Return) key. b. Modify Program 8.6 to read and display the data stored in the text.dat file created in Exercise 3a.

4. (Practice) Determine the OS command or procedure your computer provides to display the contents of a saved file.

5. (Data Processing) a. Create a text file employee.dat containing the following data:

| Name | Initial | ID | Rate | Date |
|---|---|---|---|---|
| Anthony | A | 10031 | 7.82 | 12/18/2008 |
| Burrows | W | 10067 | 9.14 | 06/09/2006 |
| Fain | B | 10083 | 8.79 | 05/18/2007 |
| Janney | P | 10095 | 10.57 | 09/28/2008 |
| Smith | G | 10105 | 8.50 | 12/20/2007 |

b. Write a C++ program to read the employee.dat file created in Exercise 5a and produce a duplicate copy of the file named employee.bak. c. Modify the program written in Exercise 5b to accept the names of the original and duplicate files as user input. d. The program written for Exercise 5c always copies data from an original file to a duplicate file. What's a better method of accepting the original and duplicate filenames, other than prompting the user for each time the program runs?

6. (Data Processing) a. Write a C++ program that opens a file and displays its contents with line numbers. That is, the program should print the number 1 before displaying the first line, the number 2 before displaying the second line, and so on for each line in the file. b. Modify the program written in 6a to list the file contents on the printer.

7. (Data Processing) a. Create a text file containing the following data (without the headings):

| Name | Social Security Number | Hourly Rate | Hours Worked |
|---|---|---|---|
| B Caldwell | 555-2222 | 7.32 | 37 |
| D Mech | 555-4444 | 8.32 | 40 |
| R Potter | 555-6666 | 6.54 | 40 |
| W Rosen | 555-8888 | 9.80 | 35 |

b. Write a C++ program that reads the data file created in 7a and computes and displays a payroll schedule. The output should list the Social Security number, name, and gross pay for each person, calculating gross pay as Hourly Rate × Hours Worked.

8. (Data Processing) a. Create a text file containing the following data (without the headings):

| Car Number | Miles Driven | Gallons of Gas Used |
|---|---|---|
| 54 | 250 | 19 |
| 62 | 525 | 38 |
| 71 | 123 | 6 |
| 85 | 1322 | 86 |
| 97 | 235 | 14 |

b. Write a C++ program that reads the data file created in 8a and displays the car number, miles driven, gallons of gas used, and per gallon (mpg) for each car. The output should contain the total miles driven, total gallons of gas, and average mpg for all cars. These totals should be displayed at the end of the output report.

9. (Data Processing) a. Create a text file with the following data (without the headings):

| Part Number | Initial Amount | Quantity Sold | Minimum Amount |
|---|---|---|---|
| QA310 | 95 | 47 | 50 |
| CM145 | 320 | 162 | 200 |
| MS514 | 34 | 20 | 25 |
| EN212 | 163 | 150 | 160 |
