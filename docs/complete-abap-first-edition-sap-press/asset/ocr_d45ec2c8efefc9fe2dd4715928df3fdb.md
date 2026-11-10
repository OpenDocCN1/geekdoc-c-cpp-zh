We’ll first look at how sequential files can be saved to the application server directories from the ABAP program and how to read the saved files to be processed in ABAP programs in Section 11.3.1. Then, in Section 11.3.2, we’ll discuss exporting and importing files from and to the presentation layer.

# 11.3.1  Working with Files in the Application Server

We use different ABAP statements to transfer data to a file stored in the application server directory. We typically perform two kinds of operations with files stored in the application server directory:

+   1. Read the file from the application server directory to an ABAP program (inbound interface)
+   2. Transfer the file from the ABAP program to the application server directory (outbound interface)

In an *inbound interface*, the data is read from the file and transferred to an internal table for further processing in the ABAP program. Conversely, in an *outbound interface*, the data from an internal table in the ABAP program is transferred to the file in the application server.

The following ABAP statements are used to read and write the files in the application server:

+   - **OPEN DATASET**
+     Opens the file for access. The system performs certain implicit authorization checks to ensure the user has the required permissions to access the file. Up to one hundred files can be opened per internal session. This statement will result in a catchable exception if the file is already opened in the program. The access type for which the file is to be opened should be supplied. The file can be opened for the following:

+   - For Input: Opens the file for reading.
+   - For Output: Opens the file for writing.
+   - Appending: Opens the file for appending data. If the file exists, the file is opened and the cursor points to the end of the line to append new lines. If the file doesn’t exist, a new file is created.
+   - Update: Opens the file for modifying the existing content.