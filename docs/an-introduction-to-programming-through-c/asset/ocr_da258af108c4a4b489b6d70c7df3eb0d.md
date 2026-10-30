This will create a single int variable x, and two initialized arrays, squares of length 5, and cubes of length 4.

Of course, it might be more convenient to initialize arrays separately from their definitions, especially if they are large. So if we wanted a large table of squares, it might be more convenient to write:

```
int squares[100]
for (int i=0; i<100; i++)
    squares[i] = i * i;
```

# 13.2 Examples of use

The common use of arrays is to store values of the same type, e.g. velocities of particles, marks obtained by students, lengths of roads, times at which trains leave, and so on. You could also say that an array is perfect to store any sequence x1,x2,...,xn. Of course, since array indices start at 0 in C++, it is more convenient to call the sequence x0,x1,...,xn-1, and then store xi in ith element of a length n array. As will be discussed in Section 14.1, an array can be used to store text. An array can also be used to store a machine language program: the ith element of the array storing the ith word of the program (Section 2.8). We will see many such uses in the rest of this chapter and the following chapters.

In this section we give some typical examples of programs that use arrays. You will see some standard programming idioms for dealing with arrays.

# 13.2.1 Notation for subarrays

It will be convenient to have some notation to indicate subarrays of an array. Thus, we will use the notation A[i...j] to mean elements A[k] of the array A where i ≤ k and k ≤ j. Note that if i > j, then the subarray is empty.

This notation is only for convenience in discussions, it is not supported by C++ and cannot be used in programs.

# 13.2.2 A marks display program

Suppose a teacher wants to announce the marks the students in a class have got. One way would be to put up a list on the school notice board. Another possibility is as follows. The teacher loads the marks onto a computer. Then any student that wants to know his marks types his roll number, and the computer displays the marks. Can we write a program to do this?

For simplicity, let us assume that there are 100 students in the class, and their roll numbers are between 1 and 100. Let us also stipulate that the program must print out the marks of each student whose roll number is entered, until the value -1 is supplied as the roll number. At this point, the program must halt.