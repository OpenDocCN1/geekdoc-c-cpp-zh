# 10.1 Introduction to File Input and Output 383

```
6 Open myfile "philosophers.dat"
8 // Write the names of three philosophers
9 // to the file.
10 Write myfile "John Locke"
11 Write myfile "David Hume"
12 Write myfile "Edmund Burke"
13
14 // Close the file.
15 Close myfile
```

The statement in line 2 declares the nameFile as the internal name for an output file. Line 6 opens the file philosophers.dat on the disk and creates an association between the file and the internal name myfile. This will allow us to use the name myfile to work with the file philosophers.dat.

The statements in lines 10 through 12 write three items to the file. Line 10 writes the string "John Locke", Line 11 writes the string "David Hume", and 12 writes the string "Edmund Burke". Line 15 closes the file. If this were an actual program and executed, the three items shown in Figure 10-5 would be written to philosophers.dat.

**Figure 10-5** Contents of the file philosophers.dat

| John Locke | David Hume | Edmund Burke |
|--- |--- |--- |
| Beginning of the file | | End of the file |

Notice that the items in the file appear in the same order that they were written by the program. "John Locke" is the first item, "David Hume" is the second item, and "Edmund Burke" is the third item. You will see the significance of this when we read data from the file momentarily.

# Delimiters and the EOF Marker

Figure 10-5 shows that three items were written to the philosophers.dat file. In most programming languages, the actual contents of the file would be more complex than the figure shows. In many languages, a special character is a delimiter written after each item. A *delimiter* is simply a predefined character or set of characters that marks the end of each piece of data. The delimiter's purpose is to separate the different items that are stored in a file. The exact character or set of characters used as delimiters varies from system to system.

In addition many systems write a special character or set of characters, known as an *end-of-file (EOF) marker*, at the end of the file. The purpose of the EOF marker is to indicate where the file's contents end. The character that is used as the EOF marker varies among different systems. Figure 10-6 shows the layout of the philosophers.dat file, with delimiters and an EOF marker.