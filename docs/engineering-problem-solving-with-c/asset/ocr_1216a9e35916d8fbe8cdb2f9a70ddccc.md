device and standard output device, respectively. Another standard stream class object that we will use in this chapter, and the following chapters, is **cerr**. The stream object **cerr** is defined by the compiler to stream output to the system's **standard error** device. **cerr** is an unbuffered stream meaning that the output will be streamed directly to standard error. Buffered streams, such as **cout**, stream data to a buffer, and the data is displayed when the buffer is flushed. A program must include the header file `iostream` to use these standard streams.

When working with data files, new streams must be defined that support the general properties of reading (>>) and writing (<<) and also support the ability to be attached to a specific file. The C++ Standard Library provides **file stream classes** to support file input and file output. The `ifstream` class is used to define input file streams that can stream data from a file, and the `ofstream` class is used to define output file streams that can stream output to a file. A portion of the C++ stream class hierarchy is illustrated in Figure 5.1.

![](bbox=[0.22, 0.34, 0.65, 0.6])

# Figure 5.1 C++ stream class hierarchy.

Figure 5.1 uses directed arrows to indicate that `ios` inherits from `ios_base`. Both `istream` and `ostream` inherit from `ios`, and `ifstream` and `ofstream` are derived from `istream` and `ostream` respectively. We also see that `iostream` inherits from both `istream` and `ostream`. This is an example of **multiple inheritance**. We will discuss the `ifstream` class and the `ofstream` class in the following sections, but first we will illustrate the use of these classes in program Chapter5_1. To use the `ifstream` and `ofstream` classes, a program must include the header file `fstream`. Program Chapter5_1 also uses the C++ standard library function `exit()`. The function `exit()` requires a single integer argument. Like the return value of `main()`, `exit()` returns its integer argument to the system. Thus, a call to `exit(1)` in the following program will terminate the program and return a value of 1 as the return value of `main()`.

```
/* Program 5_1                                                        */
/*                                                                    */
/* This program reads data pairs from the                            */
/* the file sensor.txt and writes valid data pairs                    */
*/
```