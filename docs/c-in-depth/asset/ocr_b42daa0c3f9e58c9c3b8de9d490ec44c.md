# Chapter 11

# Files

The input and output operations that we have performed so far were done through screen and keyboa only. After termination of program, all the entered data is lost because primary memory is volatile. the data has to be used later, then it becomes necessary to keep it in permanent storage device. C suppor the concept of files through which data can be stored on the disk or secondary storage device. Ti stored data can be read whenever required. A file is a collection of related data placed on the disl

The file handling in C can be broadly categorized in two types-

+   - High level(standard files or stream oriented files)
+   - Low level(system oriented files)

High level file handling is managed by library functions while low level file handling is managed by syste calls. The high level file handling is commonly used since it is easier to manage and hides most of th details from the programmer. In this chapter we'll discuss about high level file handling only.

The header file stdio.h should be included in the program to make use of the I/O functions. We hav already performed I/O with screen and keyboard using functions like scanf( ), printf( ), gets( ), puts( getchar( ) and putchar( ). The advantage of using stream oriented file I/O is that the I/O in files somewhat similar to the screen, keyboard I/O. For example we have functions like fscanf( ), fprintf( fgets( ), fputs( ) which are equivalent to the functions that we have studied earlier.

# 11.1 Text And Binary Modes

There are two ways of storing data in files, binary format and text format. In text format, data is stor as lines of characters with each line terminated by a newline character('\n'). In binary format, data stored on the disk in the same way as it is represented in the computer memory. Unix system do not make any distinction between text file and binary files.

Text files are in human readable form and they can be created and read using any text editor, whi binary files are not in human readable form and they can be created and read only by specific program written for them. The binary data stored in the file can't be read using a text editor.

The integer 1679 will take only 2 bytes in a binary file while it will occupy 4 bytes in a text file beca in binary file it is stored as an integer while in text file it is stored as a sequence of 4 characters i. '1', '6', '7', '9'.

The hexadecimal value of 1679 is 0x068F, so in binary format it is represented by the two bytes 0x and 0x8F. In a text file, this number 1679 is represented by the bytes 0x31, 0x36, 0x37, 0x39(ASC values).