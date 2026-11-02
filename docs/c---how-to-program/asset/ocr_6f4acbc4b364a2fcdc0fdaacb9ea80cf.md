# ### Section 11.8 Reading Data from a Random-Access File

+   - Function `fread` reads a specified number of bytes from a file into memory.
+   - Function `fread` can be used to read several fixed-size array elements by providing a pointer to the array in which the elements will be stored and by indicating the number of elements to be read.
+   - Function `fread` returns the number of items it successfully input. If this number is less than the third argument in the function call, then a read error occurred.

# ## Self-Review Exercises

+   11.1 Fill in the blanks in each of the following:
+      a) Function ______ closes a file.
+      b) The ______ function reads data from a file in a manner similar to how `scanf` reads from `stdin`.
+      c) Function ______ reads a character from a specified file.
+      d) Function ______ reads a line from a specified file.
+      e) Function ______ opens a file.
+      f) Function ______ is normally used when reading data from a file in random-access applications.
+      g) Function ______ repositions the file position pointer to a specific location in the file.

+   11.2 State which of the following are *true* and which are *false*. If false, explain why.
+      a) Function `fscanf` cannot be used to read data from the standard input.
+      b) You must explicitly use `fopen` to open the standard input, standard output and standard error streams.
+      c) A program must explicitly call function `fclose` to close a file.
+      d) If the file position pointer points to a location in a sequential file other than the beginning of the file, the file must be closed and reopened to read from the beginning of the file.
+      e) Function `fprintf` can write to the standard output.
+      f) Data in sequential-access files is always updated without overwriting other data.
+      g) It's not necessary to search through all the records in a random-access file to find a specific record.
+      h) Records in random-access files are not of uniform length.
+      i) Function `fseek` may seek only relative to the beginning of a file.

+   11.3 Write a single statement to accomplish each of the following. Assume that each of these statements applies to the same program.
+      a) Write a statement that opens the file `"oldmast.dat"` for reading and assigns the returned file pointer to `ofPtr`.
+      b) Write a statement that opens the file `"trans.dat"` for reading and assigns the returned file pointer to `tfPtr`.
+      c) Write a statement that opens the file `"newmast.dat"` for writing (and creation) and assigns the returned file pointer to `nfPtr`.
+      d) Write a statement that reads a record from the file `"oldmast.dat"`. The record consists of integer `accountNum`, string `name` and floating-point `currentBalance`.
+      e) Write a statement that reads a record from the file `"trans.dat"`. The record consists of the integer `accountNum` and floating-point `dollarAmount`.
+      f) Write a statement that writes a record to the file `"newmast.dat"`. The record consists of the integer `accountNum`, string `name` and floating-point `currentBalance`.

11.4 Find the error in each of the following program segments and explain how to correct it.

+   a) The file referred to by `tfPtr` (`"payables.dat"`) has not been opened.

```
printf(fPtr, "%d%s%f\n", account, company, amount);
```