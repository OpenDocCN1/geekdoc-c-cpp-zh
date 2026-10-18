# Streams as Arguments to Functions

Stream parameters must be call-by-reference

A stream can be an argument to a function. The only restriction is that the function formal parameter must be call-by-reference. A stream parameter cannot be a call-by-value parameter. For example, the function makeNeat in Display 6.6 has two stream parameters: one is of type ifstream and is for a stream connected to an input file; another is of type ofstream and is for a stream connected to an output file. We will discuss the other features of the program in Display 6.6 in the next two subsections.

# PROGRAMMING TIP Checking for the End of a File

> That's all there is, there isn't any more.

ETHEL BARRYMORE (1879–1959)

When you write a program that takes its input from a file, you will often want the program to read all the data in the file. For example, if the file contains numbers, you might want your program to calculate the average of all the numbers in the file. Since you might run the program with different data files at different times, the program cannot assume it knows how many numbers are in the file. You would like to write your program so that it keeps reading numbers from the file until there are no more numbers left to be read. If inStream is a stream connected to the input file, then the algorithm for computing this average can be stated as follows:

```
double next, sum = 0;
int count = 0;
while (There are still numbers to be read)
{
    inStream >> next;
    sum = sum + next;
    count++;
}
The average is sum / count.
```

This algorithm is already almost all C++ code, but we still must express the following test in C++:

```
(There are still numbers to be read)
```

Even though it may not look correct at first, one way to express the aforementioned test is the following:

```
(inStream >> next)
```

This technique is generally the preferred way to test for the end of the file. It reads a value from the stream and if there is nothing left to read then the