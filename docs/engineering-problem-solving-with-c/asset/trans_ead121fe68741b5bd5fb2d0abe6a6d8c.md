

```
//Get name of input file from the user
cout << "Input complete file name: " << endl;
cin >> filename;
//Attempt to open input file
fin.open(filename);
if(fin.fail())
{
    do
    {
        cerr << "Error opening input file " << filename << endl;
        cerr << "Would you like to enter a new filename? "
             << " Enter y for yes ";
        cin >> ch;
        //if the response is not yes, exit
        if(toupper(ch) != 'Y')
        {
            exit(1);
        }
        else
        {
            cerr << "Input complete file name " << endl;
            cin >> filename;
            fin.clear(); //clear current error state
            //Attempt to open input file
            fin.open(filename);
        }
    } while (fin.fail());
}
//end if
cout << filename << " has been successfully opened..." << endl;
```

Once an input file stream has been defined and successfully attached to a data file, it can be used in the same way that cin is used. Given the example above, if each line in the input file attached to fin after a successful open contains two numeric values, we can read one line of input and store the values in the variables x and y with the following statement:

```
fin >> x >> y;
```

If the input file contains character data, fin can use the get() function with a character variable as shown in the following statement:

```
fin.get(ch);
```

Note that we can read the entire file by placing the above statement inside a while (!fin.eof()) loop.

![](img/0235a4ea835dc4575bd036e024a533b3_224_0.png)

When reading information from a data file, print a few lines of the information to be sure that the data are being read correctly.

![](img/0235a4ea835dc4575bd036e024a533b3_225_0.png)

Figure 5.2 Open a data file for input.

## ofstream Class

The ofstream class is derived from the ostream class, thus it inherits all of the functionality of the ostream class. Additional member functions required to open and close data files are also provided in the ostream class.

A type declaration statement is used to define an object of type ofstream, as in

```
ofstream balloon;
```

After an ofstream object is defined, it must be associated with a specific file. The ofstream class includes a member function named open(). This function is called by the ofstream object and a file name is passed as an argument to this function. Thus, the following statement specifies that the ofstream object balloon will write data to a file named balloon.dat:

```
balloon.open("balloon.dat");
```

It is also possible to initialize an ofstream object at the time it is defined, as in

```
ofstream balloon("balloon.dat");
```

When an ofstream object calls the open() function, a new file with the specified name is created if a file by that name does not already exist. If the file already exists, it is opened and the old contents of the file are overwritten by the new data. It is possible to open an existing file for output and append new data to the end of the existing data by adding a second argument to the open function, as in

```
balloon.open("balloon.dat", ios::app);
```

Because the open() function defined in the ofstream class creates a new file if an existing file does not already exist, it is rare to have an error occur when opening a file for output. For this reason we will not check the state of an ofstream object after opening a file in the remainder of our example programs.

Once an ofstream object has been defined and associated with a data file, the ofstream object can be used in the same way that cout is used. As an example, consider the program developed in Chapter 3 that computed and printed a table of time, altitude, and velocity data. If we wanted to modify this program so that it generated a data file containing this set of data, we could use the ofstream object balloon that has been associated with an output file named balloon.dat using these statements:

```
balloon << time << " " << altitude << " " << velocity/3600 << endl;
```

A blank space is used to separate the values, and the endl manipulator causes a skip to a new line after each group of three values is written to the file.

The close() function is used to close a file after we are finished with it; the function is called a file stream object. To close the two files used in these example statements, we use the following statements:

```
sensor1.close();
balloon.close();
```

If a file has not been closed when the return 0 statement is executed, it will be closed automatically. A call to exit() will also close all files.

A string object is often used to specify the name of a data file because we frequently use the same program with different data files. It is often desirable to prompt the user to enter the name of a data file at run time and store the name of the file as a string object. This string can then be used by the open() function as illustrated in the following code segment:

```
...
string filename;
cout << "enter the name of the output file";
cin >> filename;
balloon.open(filename);
...
```

We declared filename to be a string object, since these are easy to work with. Note: In older compilers, the open() function requires a C-style string as an argument, so filename must call the function c_str(). The function c_str() is a member function of the string class, and it returns a C-style string that is equivalent to the calling object.

## Modify 5.1

These problems relate to program chapter5_1 and the flowchart in Figure 5.2 developed in this section.

- 1. Modify program chapter5_1 to read 5 data pairs from standard input. Replace the while (!fin.eof()) loop with a for loop.
- 2. Write a complete C++ program to implement the flowchart in Figure 5.2.
- 3. Modify the flowchart in Figure 5.2 to read every character from the input file after a successful open, and print the characters to standard output. Write a C++ program to implement the modified flowchart and test your program on the sensor.txt data file described on page 184.
- 4. Modify the Program in problem 3 by using fin >> ch; instead of fin.get(ch); How does this affect your output?
- 5. Modify the Program in problem 3 to write the output to a file named Chapter5Output.txt.
- 6. Modify the flowchart in Figure 5.2 to limit the number of unsuccessful tries to three. After three unsuccessful attempts to open a data file, the program should exit. Write a complete C++ program to implement the flowchart.

## 5.2 Reading Data Files

To read information from a data file, we must first know some details about the file. Obviously, we must know the file name so that we can open the file. We must also know the order and data type of the values stored in the file so that we can declare corresponding identifiers correctly. Finally, we need to know if there is any special information in the file to help us determine how much information is in the file. If we attempt to execute an input statement after we have read all the data in the file, the value of the input object will remain unchanged. This may cause unexpected results in our program. To avoid this situation, we need to know when we have read all the data.

Data files generally have one of three common structures. Some files have been generated such that the first line in the file contains the number of lines (also called records) with information that follow. For example, suppose that a file containing sensor data has 150 sets of time and sensor information. The data file could be constructed so that the first line contains only the value 150, and that line then would be followed by 150 lines containing the sensor data. To read the data from this file, we use a counter-controlled loop, as discussed in Chapter 4.

trailer signal

Another form of file structure uses a trailer signal or sentinel signal. These signals are special data values that are used to indicate or signal the last record of a file. For example, the sensor data file constructed with a sentinel signal would contain the 150 lines of information followed by a line with special values, such as -999.0 for the time and sensor value. These sentinel signals must be values that could not appear as regular data in order to avoid confusion. To read data from this type of file, we use a while loop, as discussed in Chapter 4.

