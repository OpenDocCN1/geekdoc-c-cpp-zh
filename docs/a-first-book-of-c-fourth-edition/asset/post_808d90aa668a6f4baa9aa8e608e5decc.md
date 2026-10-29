
# Program 9.6

```
#include <iostream>
#include <fstream>
#include <cstdlib>  // needed for exit()
#include <string>  // needed for the string class
using namespace std;

int main()
{
    string filename = "prices.dat";  // put the filename up front
    string line;
    ifstream inFile;

    inFile.open(filename.c_str());

    if (inFile.fail())  // check for successful open
    {
        cout << "\nThe file was not successfully opened"
             << "\n Please check that the file currently exists."
             << endl;
        exit(1);
    }

    // read and display the file's contents
    while (getline(inFile,line))
        cout << line << endl;

    inFile.close();

    return 0;
}
```

Program 9.6 is a line-by-line text-copying program, which reads a line of text from the file and then displays it on the screen. This program's output is the following:

Mats 39.95
Bulbs 3.22
Fuses 1.08

If obtaining the description and price as separate variables is necessary, either Program 9.5 should be used, or the string returned by getline() in Program 9.6 must be processed further to extract the separate data items. (See Section 9.7 for parsing procedures.)

## Point of Information

## The get() and putback() Methods

All input streams have access to the fstream class's get() method, used for character-by-character input from an input stream. This method works similarly to character extraction, using the >> operator, with two important differences: If a newline character, '\n', or a blank character, ' ', is encountered, these characters are read in the same manner as any other alphanumeric character. The syntax of this method call is the following:

```
istreamName.get(characterVariable);
```

For example, the following code can be used to read the next character from the standard input stream and store the character in the variable ch:

```
char ch;
 cin.get(ch);
```

Similarly, if inFile is an ifstream object that has been opened to a file, the following code reads the next character in the stream and assigns it to the character variable keycode:

```
char keycode;
 inFile.get(keycode);
```

In addition to the get() method, all input streams have a putback() method for putting the last character read from an input stream back on the stream. This method has the following syntax (with characterExpression representing any character variable or character value):

```
ifstreamName.putback(characterExpression);
```

The putback() method provides output capability to an input stream. The putback character need not be the last character read; it can be any character. All putback characters, however, have no effect on the data file. They affect only the open input stream. Therefore, the data file characters remain unchanged, although the characters subsequently read from the input stream can change.

## Standard Device Files

The file stream objects you have seen so far have been logical file objects. A logical file object is a stream that connects a file of logically related data, such as a data file, to a program. In addition, C++ supports a physical file object, which is a stream that connects to a hardware device, such as a keyboard, screen, or printer.

The actual physical device assigned to your program for data entry is formally called the standard input file. Usually, it's the keyboard. When a cin object method call is encountered in a C++ program, it's a request to the OS to go to this standard input file for the expected input. Similarly, when a cout object method call is encountered, the output is automatically displayed

or "written to" a device that has been assigned as the standard output file. For most systems, it's a computer screen, although it can also be a printer.

When a program including the iostream header file is executed, the standard input stream cin is connected to the standard input device. Similarly, the standard output stream cout is connected to the standard output device. These two object streams are available for programmer use, as are the standard error stream, cerr, and the standard log stream, clog. Both these streams connect to the screen.

## Other Devices

The keyboard, display, error, and log streams are connected automatically to the stream objects cin, cout, cerr, and clog when the iostream header file is included in a program. Other devices can be used for input or output if the name the system assigns is known. For example, most PCs assign the name prn to the printer connected to the computer. For these computers, a statement such as outfile.open("prn") connects the printer to the ofstream object named outfile. A subsequent statement, such as outfile << "Hello World!";, would cause the string Hello World! to be output directly to the printer. As the name of an actual file, prn must be enclosed in double quotation marks in the open() method call.

## EXERCISES 9.2

- 1. (Practice and Modify) a. Enter and run Program 9.5.
  b. Modify Program 9.5 to use the expression inFile.eof() in place of the expression inFile.good(), and run the program to see whether it operates correctly.

- 2. (Practice and Modify) a. Enter and run Program 9.6.
  b. Modify Program 9.6 by replacing cout with cerr, and verify that the output for the standard error file stream is the screen.
  c. Modify Program 9.6 by replacing cout with clog, and verify that the output for the standard log stream is the screen.

- 3. (Practice and Modify) a. Write a C++ program that accepts lines of text from the keyboard and writes each line to a file named text.dat until an empty line is entered. An empty line is a line with no text that's created by pressing the Enter (or Return) key.
  b. Modify Program 9.6 to read and display the data stored in the text.dat file created in Exercise 3a.

- 4. (Practice) Determine the OS command or procedure your computer provides to display the contents of a saved file.

- 5. (Program) a. Create a text file named employee.dat containing the following data:

| Anthony | A | 10031 | 11.82 | 12/18/2010 |
| Burrows | W | 10067 | 12.14 | 6/9/2011 |
| Fain | B | 10083 | 10.79 | 5/18/2011 |
| Janney | P | 10095 | 12.57 | 9/28/2008 |
| Smith | G | 10105 | 9.50 | 12/20/2006 |

  b. Write a C++ program to read the employee.dat file created in Exercise 5a and produce a duplicate copy of the file named employee.bak.
  
  c. Modify the program written in Exercise 5b to accept the names of the original and duplicate files as user input.
  
  d. The program written for Exercise 5c always copies data from an original file to a duplicate file. What’s a better method of accepting the original and duplicate file filenames, other than prompting the user for them each time the program runs?

- 6. (Program)
  
  a. Write a C++ program that opens a file and displays its contents with line numbers. That is, the program should print the number 1 before displaying the first line, print the number 2 before displaying the second line, and so on for each line in the file.
  
  b. Modify the program written in Exercise 6a to list the file’s contents on the printer assigned to your computer.

- 7. (Program)
  
  a. Create a text file named info.dat containing the following data (without the headings):

| Name | Social Security Number | Hourly Rate | Hours Worked |
|---|---|---|---|
| B Caldwell | 555-88-2222 | 10.50 | 37 |
| D Memcheck | 555-77-4444 | 12.80 | 40 |
| R Potter | 555-77-6666 | 16.54 | 40 |
| W Rosen | 555-99-8888 | 11.80 | 35 |

  b. Write a C++ program that reads the data file created in Exercise 7a and computes and displays a payroll schedule. The output should list the Social Security number, name, and gross pay for each person, calculating gross pay as *Hourly Rate × Hours Worked*.

- 8. (Program)
  
  a. Create a text file named car.dat containing the following data (without the headings):

| Car Number | Miles Driven | Gallons of Gas Used |
|---|---|---|
| 54 | 250 | 19 |
| 62 | 525 | 38 |
| 71 | 123 | 6 |
| 85 | 1322 | 86 |
| 97 | 235 | 14 |

  b. Write a C++ program that reads the data in the file created in Exercise 8a and displays the car number, miles driven, gallons of gas used, and miles per gallon (mpg) for each car. The output should contain the total miles driven, total gallons of gas used, and average mpg for all cars. These totals should be displayed at the end of the output report.
