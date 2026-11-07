
Consider the binary number $1111101010001010101_2$. Now,

$1111101010001010101_2 = 111\ 1101\ 0100\ 0101\ 0101_2$

$\qquad\qquad\qquad\quad = 0111\ 1101\ 0100\ 0101\ 0101_2$, add one zero to the left

$\qquad\qquad\qquad\quad = 7D455_{16}$

Hence, $1111101010001010101_2 = 7D455_{16}$.

Next, to convert a hexadecimal number into an equivalent binary number, write the four-digit binary representation of each hexadecimal digit into that number. For example,

$A7F32_{16} = 1010\ 0111\ 1111\ 0011\ 0010_2$

$\qquad\qquad = 10100111111100110010_2$

Thus, $A7F32_{16} = 10100111111100110010_2$.

## More on File Input/Output

In Chapter 3, you learned how to read data from and write data to a file. This section expands on the concepts introduced in that chapter.

### Binary Files

In Chapter 3, you learned how to make a program read data from and write data to a file. However, the files that the programs have used until now are called text files. Data in a text file is stored in the character format. For example, consider the number 45. If 45 is stored in a file, then it is stored as a sequence of two characters—the character '4' followed by the character '5'. The eight-bit machine representation of '4' is 00110100 and the eight-bit machine representation of '5' is 00110101. Therefore, in a text file, 45 is stored as 0011010000110101. When this number is read by a C++ program, it must first be converted to its binary format. Suppose that the integers are represented as 16-bit binary numbers. The 16-bit binary representation of 45 is then 0000000000101101. Similarly, when a program stores the number 45 in a text file, it first must be converted to its text format. It thus follows that reading data from and writing data to a text file is not efficient, because the data must be converted from the text to the binary format and vice versa.

On the other hand, when data is stored in a file in the binary format, reading and writing data is faster, because no time is lost in converting the data from one format to another format. Such files are called binary files. More formally, **binary files** are files in which data is stored in the binary format. Data in a text file is also called **formatted data**, and in a binary file it is called **raw data**.

C++ allows a programmer to create binary files. This section explains how to create binary files and also how to read data from binary files.

To create a binary file, the file must be opened in the binary mode. Suppose `outFile` is an `ofstream` variable (object). Consider the following statement:

```cpp
outFile.open("employee.dat", ios::binary);
```

This statement opens the file `employee.dat`. Data in this file will be written in its binary format. Therefore, the file opening mode `ios::binary` specifies that the file is opened in the binary mode.

Next, you use the stream function `write` to write data to the file `employee.dat`. The syntax to use the function `write` is:

```cpp
fileVariableName.write(reinterpret_cast<const char *> (buffer),
                      sizeof(buffer));
```

where fileVariableName is the object used to open the output file, and the first argument buffer specifies the starting address of the location in memory where the data is stored. The expression `sizeof(buffer)` specifies the size of the data, in bytes, to be written.

For example, suppose num is an int variable. The following statement writes the value of num in the binary format to the file associated with outFile:

```cpp
outFile.write(reinterpret_cast<const char *> (&num),
             sizeof(num));
```

Similarly, suppose empSalary is an array of, say, 100 components and the component type is double. The following statement writes the entire array to the file associated with outFile:

```cpp
outFile.write(reinterpret_cast<const char *> (empSalary),
             sizeof(empSalary));
```

Next, let us discuss how to read data from a binary file. The operation of reading data from a binary file is similar to writing data to a binary file. First, the binary file must be opened. For example, suppose inFile is an ifstream variable, and a program has already created the binary file employee.dat. The following statement opens this file:

```cpp
inFile.open("employee.dat");
```

or:

```cpp
inFile.open("employee.dat", ios::binary);
```

To read data in the binary format, the stream function `read` is used. The syntax to use the function `read` is:

```cpp
fileVariableName.read(reinterpret_cast<char *> (buffer),
                     sizeof(buffer));
```

The first argument `buffer` specifies the starting address of the location in memory where the data is to be stored. The expression `sizeof(buffer)` specifies the size of the data, in bytes, to be read.

The program in the following example further explains how to create binary files and read data from a binary file.

### EXAMPLE E-1

```cpp
//Creating and reading binary files

#include <iostream>
#include <fstream>

using namespace std;

struct studentType
{
    char firstName[15];
    char lastName[15];
    int ID;
};

int main()
{
        //create and initialize an array of students' IDs
    int studentIDs[5] = {111111, 222222, 333333,
                         444444, 555555};             //Line 1

        //declare and initialize the struct newStudent
    studentType newStudent = {"John", "Wilson",
                              777777};                 //Line 2

    ofstream outFile;                                  //Line 3

        //open the output file as a binary file
    outFile.open("ids.dat", ios::binary);              //Line 4

        //write the array in the binary format
    outFile.write(reinterpret_cast<const char *> (studentIDs),
                  sizeof(studentIDs));                 //Line 5
        //write the newStudent data in the binary format
    outFile.write(reinterpret_cast<const char *> (&newStudent),
                  sizeof(newStudent));                 //Line 6

    outFile.close();  //close the file                  //Line 7

    ifstream inFile;                                   //Line 8
    int arrayID[5];                                    //Line 9
    studentType student;                               //Line 10

    //open the input file
    inFile.open("ids.dat");                            //Line 11

    if (!inFile)                                       //Line 12
    {
        cout << "The input file does not exist. "
             << "The program terminates!!!" << endl;   //Line 13
        return 1;                                      //Line 14
    }

    //input the data into the array arrayID
    inFile.read(reinterpret_cast<char *> (arrayID),
                sizeof(arrayID));                      //Line 15
    //output the data from the array arrayID
    for (int i = 0; i < 5; i++)                        //Line 16
        cout << arrayID[i] << " ";                     //Line 17
    cout << endl;                                      //Line 18

    //read the student's data
    inFile.read(reinterpret_cast<char *> (&student),
               sizeof(student));                       //Line 19

    //output studentData
    cout << student.ID << " " << student.firstName
         << " " << student.lastName << endl;           //Line 20

    inFile.close();     //close the file               //Line 21

    return 0;                                          //Line 22
}
```

**Sample Run:**

111111 222222 333333 444444 555555
777777 John Wilson

The output of the preceding program is self-explanatory. The details are left as an exercise for you.

> **NOTE** In the program in Example E-1, the statement in Line 2 declares the `struct` variable `newStudent` and also initializes it. Because `newStudent` has three components and we want to initialize all the components, three values are specified in braces separated by commas. In other words, `struct` variables can also be initialized when they are declared.

The program in the following example further explains how to create binary files and then read the data from the binary files.
