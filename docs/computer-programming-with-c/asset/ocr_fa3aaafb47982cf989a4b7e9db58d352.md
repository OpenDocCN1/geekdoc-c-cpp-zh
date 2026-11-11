![](bbox=[0.219, 0.108, 0.789, 0.563])

The class `ifstream` is used to read the data from the file and is derived from classes `istream`. The class `ifstream` contains functions required to take the data input from the file. Similarly, class `ofstream` contains output functions required to write data to the file. The class `ofstream` is derived from the `ostream`. We can also perform input as well as output operations on a file at the same time. To support both the input as well as the output operations together, C++ has a built-in class named `fstream`. This class is derived from `iostream` class as shown in the Figure 15.15.

In summary, there are three main classes on which you need to focus on to work with the files.

+   1. `ifstream` – To be used by the program to read data from the file.
+   2. `ofstream` – To be used by the program to write data to the file.
+   3. `fstream` – To be used by the program to perform read as well as write operations on the file.

It is important to note that all of the above file handling classes is defined in the header file `fstream.h` and hence, it is very important to include `fstream.h` in the C++ program before using these classes. The next section describes some of the built-in functions defined in each of these classes to perform file I/O operations.