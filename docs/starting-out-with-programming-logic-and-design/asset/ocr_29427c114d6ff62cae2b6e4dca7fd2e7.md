# 10.1 Introduction to File Input and Output

# Closing an Input File

As previously mentioned, a program should close a file when it is finished working with it. In our pseudocode, we will use the Close statement to close input files, in the same way that we close output files. For example,

```
Close inventoryFile
```

the file that is associated with the name inventoryFile.

Program 10-2 shows the pseudocode for a program that opens the philosophers.dat file that would be created by Program 10-1, reads the three names from the file, closes the file, and then displays the names that were read. Figure 10-7 shows a flowchart for the program. Note that the Read statements are shown in parallelograms.

# Figure 10-7 Flowchart for Program 10-2

![](bbox=[0.283, 0.343, 0.715, 0.903])