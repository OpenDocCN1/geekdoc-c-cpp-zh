# 11.2 See the answers below:

+   a) False. Function fscanf can be used to read from the standard input by including the pointer to the standard input stream, stdin, in the call to fscanf.
+    b) False. These three streams are opened automatically by C when program execution begins.
+    c) False. The files will be closed when program execution terminates, but all files should be explicitly closed with fclose.
+    d) False. Function rewind can be used to reposition the file position pointer to the beginning of the file.
+    e) True.
+    f) False. In most cases, sequential file records are not of uniform length. Therefore, it's possible that updating a record will cause other data to be overwritten.
+    g) True.
+    h) False. Records in a random-access file are normally of uniform length.
+    i) False. It's possible to seek from the beginning of the file, from the end of the file and from the current location in the file.

# 11.3

```
a) ofPtr = fopen("oldmast.dat", "r");
 b) tfPtr = fopen("trans.dat", "r");
 c) nfPtr = fopen("newmast.dat", "w");
 d) fscanf(ofPtr, "%d%s%f", &account, name, &currentBalance);
 e) fscanf(tfPtr, "%d%f", &account, &dollarAmount);
 f) fprintf(nfPtr, "%d %s %.2f", account, name, currentBalance);
```

# 11.4 See the answers below:

+   a) Error: "payables.dat" has not been opened before using fPtr.
+    Correction: Use fopen to open "payables.dat" for writing, appending or updating.
+    b) Error: Function open is not a Standard C function.
+    Correction: Use function fopen.
+    c) Error: The function scanf should be fscanf. Function fscanf uses the incorrect file pointer to refer to file "payables.dat".
+    Correction: Use payPtr to refer to "payables.dat" and use fscanf.
+    d) Error: The contents of the file are discarded because the file is opened for writing ("w").
+    Correction: To add data to the file, either open the file for updating ("r+") or open the file for appending ("a" or "a+").
+    e) Error: File "courses.dat" is opened for updating in "w+" mode, which discards the current contents of the file.
+    Correction: Open the file in "a" or "a+" mode.

# Exercises

# 11.5 Fill-In the blanks in each of the following:

+   a) Large amounts of data are stored on secondary storage devices as ______.
+    b) A(n) ______ is composed of several fields.