+   15.7 When an error occurs, the variable ______ is set, and the ______ function prints the text associated with that variable.
+   15.8 The ______ function determines whether EOF was encountered by the previous function.
+   15.9 The ______ function is used to write an array or structure to disk.

# A3. MULTIPLE-CHOICE QUESTIONS

+   15.1 The filename is used as an argument by (A) **fread**, (B) **fclose**, (C) **rewind**, (D) none of these.
+   15.2 For reading and updating an existing file, **fopen** uses the mode (A) w, (B) wt, (C) r+, (D) a+.
+   15.3 To read a character from a disk file, the function to use is (A) **getc**, (B) **fgets**, (C) **getchar**, (D) none of these.
+   15.4 For sending diagnostic messages to the standard error, the function to use is (A) **fputs**, (B) **printf**, (C) **fprintf**, (D) all of these, (E) A and C.
+   15.5 The data types handled by the **fread** and **fwrite** functions are (A) all types, (B) primary, (C) derived, (D) user-defined, (E) C and D.
+   15.6 The size of a file can be determined by (A) **sizeof**, (B) **fseek**, (C) **ftell**, (D) B and C, (E) none of these.
+   15.7 Pick the odd item out: (A) **fgets**, (B) **getchar**, (C) **fseek**, (D) **rewind**.

# A4. MIX AND MATCH

15.1 Associate the following C terms with their areas of application:
(A) rb, (B) SEEK_SET, (C) FILE, (D) errno.

(1) **rewind**, (2) **fopen**, (3) wrong item, (4) structure.

# CONCEPT-BASED QUESTIONS

+   15.1 When will you use the library functions to handle files in preference to the < and > redirection features?
+   15.2 Discuss the significance of the file offset pointer when a file is read by different file-handling functions. How can this pointer be reset to the beginning of the file?
+   15.3 Explain the concept of streams and their significance in I/O operations.
+   15.4 Specify the circumstances when the fopen function can fail.
+   15.5 How do **fgets** and the scan set of **scanf** treat the newline character?
+   15.6 Discuss the circumstances that determine whether to save data with or without delimiters separating the fields.