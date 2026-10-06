# 382 Chapter 10 Files

In our pseudocode, we will use the Close statement to close a file. For example,

```
Close customerFile
```

closes the file that is associated with the name customerFile.

Program 10-1 shows the pseudocode for a sample program that opens an output file, writes data to it, and then closes it. Figure 10-4 shows a flowchart for the program. Because the Write statements are output operations, they are shown in parallelograms.

**Figure 10-4** Flowchart for Program 10-1

![](bbox=[0.403, 0.295, 0.597, 0.802])

```
**Program 10-1**
1 // Declare an internal name for an output file.
2 Declare OutputFile myFile
3
4 // Open a file named philosophers.dat on
5 // the disk.
```