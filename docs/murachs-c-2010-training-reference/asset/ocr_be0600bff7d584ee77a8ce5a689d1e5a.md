# Perspective

In this chapter, you learned how to read and write the data in text and binary files. These files can be used when you need a relatively easy way to store a limited number of records with a limited number of fields. However, when the data requirements for an application are more complex, it usually makes sense to use a database instead of text or binary files.

# Terms

+   input file
output file
I/O operations
file I/O
text file
field
record
binary file
stream
output stream
input stream
text stream
binary stream

# Exercise 21-1 Work with a text file

+   1. Open the project in the C# 2010\Chapter21\CustomerText directory. This is the Customer Maintenance application that you developed for exercise 12-1, but it doesn't save or retrieve the data.
2. In the CustomerDB class, add to use a text file to read and write a List<> of Customer objects. methods use the GetCustomers and SaveCustomers methods Unless you moved it after downloading and installing the files for this book, the path for this file should be C:\2010\FilesCustomers.txt. Then, add code to the methods in the two forms so they use the CustomerDB class to read and write the file.
3. Test the application by adding and deleting customers. To verify that the data is being saved to disk, stop the application and run it again. Use a text editor like Notepad to open the file after a test run.

# Exercise 21-2 Work with a binary file

+   1. Use Windows Explorer to copy the directory named CustomerText that you created for the previous exercise within the Chapter 21 directory. Then, rename that directory CustomerBinary, and open the project in that directory.
2. Modify the CustomerDB class so it uses a binary file named Customers.dat instead of a text file. Also, leave the signatures of the GetCustomers and SaveCustomers methods as they are so you won't need to modify the code in the form class calls these methods. Then, test the application by adding and deleting customers.