Business applications typically have to manipulate large amounts of data. This data is stored in one or more files. As you learned in Chapter 1 of *Programming Logic and Design, Fifth Edition*, data is organized in a hierarchy. At the lowest level of the hierarchy is a **field**, which is a group of characters. On the next level up is a **record**, which is a group of related fields. For example, you could write a program that processes employee records where each employee record consists of three fields: the employee’s first name, the employee’s last name, and the employee’s department number.

In C++, to use the data stored in a file, the program must first open the file and then read the data from the file. You use prewritten classes that are part of a C++ library to accomplish this. Next, you learn how to use these classes to open a file, close a file, read data from a file, and write data to a file.

# USING INPUT AND OUTPUT CLASSES

To use the classes that you need to perform file input (`ifstream`) and output (`ofstream`), you must add the following preprocessor directive at the beginning of your C++ program:

```
```cpp
#include <fstream>
```
```

The classes included in the `fstream` class are prewritten for you by the C++ development team and allow you to simplify your programming tasks by creating objects using these classes. You can then use the attributes and methods of these objects in your C++ programs.

# OPENING A FILE FOR READING

To open a file in C++ to read data into your program, you declare a file input stream object (variable) as shown below:

```
```cpp
ifstream data_in;
```
```

You then use the open method (function) to specify the name of the file to open. Look at the following example:

```
```cpp
data_in.open("inputFile.dat");
```
```

In the example, you use the `ifstream` object (`data_in`), followed by a dot (`.`), followed by the name of the method (`open`) to open a file for input. Within the parentheses, you place the name of the file you want to open enclosed in double quotes. This statement opens the file named `inputFile.dat` for reading. This means that the program can now read data from the file. In this example, the file named `inputFile.dat` must be saved in the same folder as the C++ program that is using the file. To open a file that is saved in a different folder, a path must be specified as in the next example:

```
```cpp
data_in.open("C:\\myC++Programs\\Chapter9\\inputFile.dat");
```
```

> > **NOTE**  
> > You can think of the `istream` as the data type for input files. In the next chapter, you will learn that `istream` is actually a class and `data_in` is an object.

# READING DATA FROM AN INPUT FILE

Once you have opened the input file, you are ready to read the data in the file. You can use the extraction operator `>>` just as you used it with `cin`.