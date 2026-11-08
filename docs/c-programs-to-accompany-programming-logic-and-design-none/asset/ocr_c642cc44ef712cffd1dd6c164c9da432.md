In the next example, we will assume that the input file for a program is organized so that an employee’s first name is on one line, followed by the employee’s last name on the next line, followed by his or her salary on the third, as follows:

```
Tim
Moriarty
2000.00
```

To allow the program to read this data, you would write the following C++ code:

```
ifstream data_in;
string firstName, lastName;
double salary;
data_in.open("inputFile.dat");
data_in >> firstName;
data_in >> lastName;
data_in >> salary;
```

The first line in the example declares data_in, an ifstream object. The second line declares two string variables named firstName and lastName. The third line declares a double named salary. Next, data_in is used with the open method to open the file named inputFile.dat. The extraction operator (>>) is then used three times to read the three lines of input from the file (inputFile.dat) associated with data_in. After this code executes, the variable named firstName contains the value Tim, the variable named lastName contains the value Moriarty, and the variable named salary contains the value 2000.00.

# READING DATA USING A LOOP AND EOF

In a program that has to read large amounts of data, it is usually best to use a loop. In the loop, the program continues to read from the file until EOF (end of file) is encountered. In C++, the eof method (function) returns a true value when EOF is reached and a false value when EOF has not been reached. The eof method can be used with cin for keyboard input or with an ifstream object, such as data_in.

The C++ code that follows shows how to use the eof method as part of a loop:

```
ifstream data_in;
string firstName;
data_in.open("inputFile.dat");
data_in >> firstName;
while(!(data_in.eof()))
{
    cout << firstName;
    data_in >> firstName;
}
```

> **NOTE**  
> For keyboard input, you enter the EOF character by typing Ctrl + Z (Windows) or Ctrl + D (UNIX/Linux).

In this example, a priming read is used on the fourth line, data_in >> firstName;, and then the eof method is used as the expression to be tested in the while loop. As long as the value returned by eof is not equal to true, the expression is true and the loop is entered.