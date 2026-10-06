# True or False

+   1. When working with sequential access file, you can jump directly to any piece of data in the file without reading the data that comes before it.

+   2. In most languages, when you open an output file and that file already exists on the disk, the contents of the existing file will be erased.

+   3. The process of opening a file is only necessary with input files. Output files are automatically opened when data is written to them.

+   4. The purpose of EOF marker is to indicate where a file ends. Files typically contain several EOF markers.

+   5. When an input file is opened, its read position is initially set to the first item in the file.

+   6. When a file that already exists is opened in append mode, the file's contents are erased.

+   7. In control break logic, the program performs some ongoing task (such as processing the items in a file), but permanently stops the task when a control variable reaches a specific value or changes its value.

# Short Answer

+   1. Describe the three steps that must be taken when a file is used by a program.

+   2. Why should a program close a file when it's finished using?

+   3. What is a file's read position? Where is the read position when a file is first opened for reading?

+   4. If an existing file is opened in append mode, what happens to the file's contents?

+   5. In most languages, if a file does not exist and a program attempts to open it in append mode, what happens?

+   6. What is the purpose of the e function that was discussed in this chapter?

+   7. What is control break logic?

# Algorithm Workbench

+   1. Design a program that opens an output file with the external name my_name.dat, writes your name to the file, and then closes the file.

+   2. Design a program that opens the my_name.dat file that was created by the algorithm in question 1, reads your name from the file, displays the name on the screen, and then closes the file.

+   3. Design an algorithm that does the following: opens an file with the external name number_list.dat, uses a loop to write the numbers 1 through 100 to the file, and then closes the file.