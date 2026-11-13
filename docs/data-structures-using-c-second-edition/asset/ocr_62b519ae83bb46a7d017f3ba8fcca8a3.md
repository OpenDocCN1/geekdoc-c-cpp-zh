+   * A data field is an elementary unit that stores a single fact. A data field is usually characterized by its type and size. For example, student's name is a data field that stores the name of students. This field is of type character and its size can be set to a maximum of 20 or 30 characters depending on the requirement.
+   * A record is a collection of related data fields which is seen as a single unit from the application point of view. For example, the student's record may contain data fields such as name, address, phone number, roll number, marks obtained, and so on.
+   * A file is a collection of related records. For example, if there are 60 students in a class, then there are 60 records. All these related records are stored in a file. Similarly, we can have a file of all the employees working in an organization, a file of all the customers of a company, a file of all the suppliers, so on and so forth.
+   * A directory stores information of related files. A directory organizes information so that users can find it easily. For example, consider Fig. 16.1 that shows how multiple related files are stored in a student directory.

![](bbox=[0.27, 0.36, 0.78, 0.54])

Figure 16.1 Student directory

# 16.3 FILE ATTRIBUTES

Every file in a computer system is stored in a directory. Each file has a list of attributes associated with it that gives the operating system and the application software information about the file and how it is intended to be used.

A software program which needs to access a file looks up the directory entry to discern the attributes of that file. For example, if a user attempts to write to a file that has been marked as a read-only file, then the program prints an appropriate message to notify the user that he is trying to write to a file that is meant only for reading.

Similarly, there is an attribute called hidden. When you execute the dir command in DOS, then the files whose hidden attribute is set will not be displayed. These attributes are explained in this section.

**File name** It is a string of characters that stores the name of a file. File naming conventions vary from one operating system to the other.

**File position** It is a pointer that points to the position at which the next read/write operation will be performed.

**File structure** It indicates whether the file is a text file or a binary file. In the text file, the numbers (integer or floating point) are stored as a string of characters. A binary file, on the other hand, stores numbers in the same way as they are represented in the main memory.