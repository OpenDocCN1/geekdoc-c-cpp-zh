return false. You also can call the member function `eof` on the input object to determine whether the end-of-file indicator has been entered.

Line 20 extracts each set of data into the variables `account`, `name` and `balance`, and determines whether the end-of-file indicator has been entered. When end-of-file is encountered (that is, when the user enters the end-of-file key combination) or an input operation fails, the operator bool returns false, and the while statement terminates.

Line 21 writes a set of data to the file `clients.txt`, using the stream insertion operator `<<` and the output object we associated with the file at the beginning of the program. The data may be retrieved by a program designed to read the file (see Section 8.14). The file created in Fig. 8.10 is simply a text file that can be viewed by any text editor.

# Closing a File

Once the user enters the end-of-file indicator, the `while` loop terminates. At this point, we reach the `if` statement’s closing brace, so the output object goes out of scope, which automatically closes the file. You should always close a file as soon as it’s no longer needed in a program.

# Sample Execution

In the sample execution of Fig. 8.10, we entered information for five accounts, then signaled that data entry was complete by entering the end-of-file indicator (^Z is displayed for Microsoft Windows). This dialog window does not show how the data records appear in the file. The next section shows how to create a program that reads this file and prints its contents.

# Checkpoint

+   1. **(True/False)** C++ imposes rigid structure on files and records. This makes it convenient for you to develop file-based and record-based applications quickly.
+   
+      **Answer:** False. Actually, C++ imposes no structure on files. Thus, a concept like that of a file of records, with each record containing related data items, does not exist. You structure files to meet your application’s requirements.
+   
+   2. **(True/False)** When you create an `ofstream` object, you must specify the `ios::out` file-open mode.
+   
+      **Answer:** False: The `ios::out` file-open mode is the `ofstream` constructor’s default second argument, so this open mode is not required.
+   
+   3. **(Code)** Write a statement that opens the file `inventory_report.txt` without specifying the file-open mode.
+   
+      **Answer:** `std::ofstream output{"inventory_report.txt"};`

# 8.14 Reading Data from a Sequential File

Figure 8.10 created a sequential file. Figure 8.11 reads data sequentially from the file `clients.txt` and displays the records. Creating an `ifstream` object opens a file for input. An `ifstream` is initialized with a filename and file-open mode. Line 11 creates an `ifstream` object called `input` that opens the `clients.txt` file for reading.⁶ If a file’s con-

6. The file `clients.txt` must be in the same folder as this program’s executable.