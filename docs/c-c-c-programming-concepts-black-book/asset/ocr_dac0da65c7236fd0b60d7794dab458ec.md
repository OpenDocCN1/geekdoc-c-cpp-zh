# Chapter 21

A file system stores and organizes files and their data. It typically has directories or folders that allow the grouping of similar files. Various operations, such as updating an existing file, creating a new file, and renaming a directory, can be performed on a file system. C# provides the System.IO namespace that offers various classes, methods, and properties to manipulate files and directories. For example, the System.IO namespace provides the FileStream, StreamReader, StreamWriter, File, and FileInfo classes to perform operations, such as moving, copying, and deleting files. In addition, the namespace provides the Directory and DirectoryInfo classes that can be used to create, move, and delete directories.

In this chapter, we learn about the file system architecture and various risks involved in using files in a Web application. Further, the chapter discusses various file system classes, namely FileStream, StreamReader, and StreamWriter. Next, we learn the classes, such as Directory, DirectoryInfo, File, and FileInfo, for directory and file operations. We also learn to create a file system application by using C#. In addition, the chapter discusses the file compression technique and isolated storage. Towards the end, we learn to write different types of emails using C#.

Let’s begin the chapter by exploring the architecture of a file system.

# Exploring the File System Architecture

In a file system, a file is the basic unit of resources. A file comprises metadata and textual content. Metadata can be defined as data about data. In other words, metadata specifies the information about the data or content in a file. Generally, metadata contains the following information about a file:

+   - Creation date of the file
+   - Last modification date of the file
+   - Last accessed date of the file
+   - Size of the file
+   - Location of the file in a system
+   - Type of the file

However, depending on the type of a file, other information can also be associated with the metadata. For example, metadata for a video file also contains the length of the video to define its duration.

When we create files, they are always stored inside a directory. Directory is nothing but a folder that is created to store files in it. In other words, a folder in a file system corresponds to a directory. This directory or folder may contain another set of directories or files.

A file system deals with the file storage architecture and file manipulation methods. The general services that a file system provides are:

+   - Move a file to a different location
+   - Copy a file from one location to another
+   - Delete a file from a specific location
+   - Append a file to another existing file
+   - Edit the existing file
+   - Upload a file to a specific location
+   - Create a file to a specified location
+   - Modify the structure of a file

In the next section, let’s discuss the risks involved in file systems when they are used in a Web application.