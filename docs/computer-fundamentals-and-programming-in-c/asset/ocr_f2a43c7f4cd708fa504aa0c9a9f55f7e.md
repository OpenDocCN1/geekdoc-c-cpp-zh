# Files in C

# CHAPTER 15

# Learning Objectives

![](bbox=[0.882, 0.373, 0.963, 0.424])

After studying this chapter, the readers will be able to

+   - analyse the concept of streams used in the C file system
+   - discuss text and binary files
+   - process text files as well as binary files using standard library functions
+   - explain the sequential and random access of data stored in a disk file using proper standard library functions
+   - discuss advanced file management system and low-level input and output

# 15.1 INTRODUCTION

A file is a repository of data that is stored in a permanent storage media, mainly in secondary memory. So far, data was entered into the programs through the computer’s keyboard. This is somewhat laborious if there is a lot of data to process. The solution is to combine all the input data into a file and let the C program read the information from the file when it is required. Frequently, files are used for storing information that can be processed by the programs. Files are not only used for storing data, programs are also stored in files. The editor, which is used to write or edit programs and save, simply manipulates files for the programmer. The UNIX commands cat, cp, and cmp are all programs which process the files.

In order to use files one has to learn about file I/O, i.e., how to write information to a file, and how to read information from a file. It will be seen that file I/O is almost identical to the terminal I/O that has been used so far. The primary difference between manipulating files and terminal I/O is that the programs must specify which files are to be used because there are many files on the disk. Specifying the file to use is referred to as opening the file. When one opens a file, what is to be done with the file must also be mentioned, i.e., read from the file, write to the file, or both.

to the terminal I/O that has been used so far. The primary difference between manipulating files and terminal I/O is that the programs must specify which files are to be used because there are many files on the disk. Specifying the file to use is referred to as opening the file. When one opens a file, what is to be done with the file must also be mentioned, i.e., read from the file, write to the file, or both.

A very important concept in C is the stream. The stream is a common, logical interface to the various devices that comprise the computer. In its most common form, a stream is a logical interface to a file. As defined by C, the term ‘file’ can refer to a disk file, the screen, the keyboard, a port, a file on tape, and so on. Although files differ in form and capabilities, all streams are the same. The stream provides a consistent interface to the programmer. Stream I/O uses some temporary storage area, called buffer, for reading from or writing data to a file. This is illustrated in Fig. 15.1.