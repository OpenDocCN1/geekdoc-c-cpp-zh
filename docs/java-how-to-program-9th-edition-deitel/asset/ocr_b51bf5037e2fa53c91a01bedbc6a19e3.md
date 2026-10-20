```
Enter file or directory name: E:\Program Files\Java\jdk1.6.0_11\demo\jfc
jfc exists
is not a file
is a directory
is absolute path
Last modified: 1228404395024
Length: 4096
Path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc
Absolute path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc
Parent: E:\Program Files\Java\jdk1.6.0_11\demo\jfc

Directory contents:
CodePointIM
FileChooserDemo
Font2DTest
Java2D
Laffy
Metalworks
Notepad
SampleTree
Stylepad
SwingApplet
SwingSet
SwingSet2
SwingSet3
```

```
Enter file or directory name: C:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D\README.txt
README.txt exists
is not a directory
is not a file
is absolute path
Last modified: 1228404384270
Length: 7518
Path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D\README.txt
Absolute path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D\README.txt
Parent: E:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D
```

# Fig. 17.3 | File class used to obtain file and directory information. (Part 2 of 2.)

(either as a file or as a directory) on the disk. If the name does not exist, control proceeds to lines 46–49 and displays a message to the screen containing the name the user typed, followed by “does not exist.” Otherwise, the if statement (lines 22–45) executes. The program outputs the name of the file or directory (line 27), followed by the results of testing the File object with isFile (line 28), isDirectory (line 29) and isAbsolute (line 31). Next, the program displays the values returned by lastModified (line 33), length (line 33), getPath (line 34), getAbsolutePath (line 35) and getParent (line 35). If the File object represents a directory (line 37), the program obtains a list of the directory’s contents as an array of Strings by using File method list (line 39) and displays the list on the screen.

The first output of this program demonstrates a File object associated with the jfc directory from the JDK. The second output demonstrates a File object associated with