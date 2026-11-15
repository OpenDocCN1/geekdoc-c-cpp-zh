```
File open function:
//filename is a string object
sensor1.open(filename.c_str());
balloon.open(filename.c_str());
```

```
File fail function:
if (sensor1.fail())
```

```
File input:
sensor1 >> t >> motion;
```

```
File output:
balloon << setw(8) << time << setw(8) << height << setw(8) << velocity;
```

```
Output to standard error:
cerr << "Error encountered on input";
```

```
File close function:
sensor1.close();
stream clear function
sensor1.clear()
standard error output stream
```

# Notes

+   1. Prompt the user to enter filenames so that they can be determined at run time.

# Debugging Notes

+   1. When debugging a program that reads data from a data file, print the values as soon as they are read to check for errors in reading the information.
+   2. When debugging a program that reads a data file, be sure that your program checks for successful opening of the file.
+   3. To avoid infinite loops when inputting data, check the error status of the istream object before each iteration of the loop.
+   4. To avoid problems with operating systems that are case sensitive, use filenames with lowercase letters.

# Problems

# Exam Practice!

# True/False Problems

Indicate whether the following statements are true (T) or false (F).

+   1. You can format file output in the same way as screen output. T F
+   2. When a program attempts to open a data file for input, and the file is not found, the program will terminate. T F
+   3. A program must include the head ifstream to use the standard streams. T F