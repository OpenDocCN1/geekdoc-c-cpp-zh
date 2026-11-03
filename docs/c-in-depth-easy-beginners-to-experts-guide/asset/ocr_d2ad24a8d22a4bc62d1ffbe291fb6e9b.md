![](bbox=[0.32, 0.08, 0.68, 0.27])

# CHAPTER

# ∞ 12 ∞

# (File handling through C)

# Introduction-

Until now, we have used the functions scanf and printf to read and write data. These are console oriented input and output functions which always use the keyboard and screen as the target place. It is fine until the data is small. However in real life problems involve large volumes of data and in such cases the console oriented output and input operations has two major problems:

A. It is time consuming to handle a large amount of data.
B. The entire data is lost as soon as the program is closed or computer is switched off. To overcome these problems we use file handling. File can be used to store the data in the hard disk so that the data is permanently saved and does not get deleted even if the computer is switched off.

A file can be defined as a place on the disk where a group of related data is stored. A number of functions can be performed on the files:

+   - Naming a file.
+   - Opening a file.
+   - Reading data from a file.