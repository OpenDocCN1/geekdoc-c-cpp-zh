**Caution**

In the past, the usual tests for successful opening of a file were the following:

```
```cpp
if(fin.fail()) ... // failed to open
if(!fin.good()) ... // failed to open
if (!fin) ... // failed to open
```
```

The fin object, when used in a test condition, is converted to false if fin.good() is false and to true otherwise, so the two forms are equivalent. However, these tests fail to detect one circumstance, which is attempting to open a file by using an inappropriate file mode (see the “File Modes” section, later in this chapter). The is_open() method catches this form of error, along with those caught by the good() method. However, older C++ implementations do not have is_open().

# Opening Multiple Files

You might require that a program open more than one file. The strategy for opening multiple files depends on how they will be used. If you need two files open simultaneously, you must create a separate stream for each file. For example, a program that collates two sorted files into a third file would create two ifstream objects for the two input files and an ofstream object for the output file. The number of files you can open simultaneously depends on the operating system.

However, you may plan to process a group of files sequentially. For example, you might want to count how many times a name appears in a set of 10 files. In this case, you can open a single stream and associate it with each file in turn. This conserves computer resources more effectively than opening a separate stream for each file. To use this approach, you declare an ifstream object without initializing it and then use the open() method to associate the stream with a file. For example, this is how you could handle reading two files in succession:

```
```cpp
ifstream fin;                 // create stream using default constructor
fin.open("fat.txt");          // associate stream with fat.txt file
...
fin.close();                  // terminate association with fat.txt
fin.clear();                  // reset fin (may not be needed)
fin.open("rat.txt");          // associate stream with rat.txt file
...
fin.close();
```
```

We’ll look at an example shortly, but first, let’s examine a technique for feeding a list of files to a program in a manner that allows the program to use a loop to process them.

# Command-Line Processing

File-processing programs often use command-line arguments to identify files. *Command-line arguments* are arguments that appear on the command line when you type a