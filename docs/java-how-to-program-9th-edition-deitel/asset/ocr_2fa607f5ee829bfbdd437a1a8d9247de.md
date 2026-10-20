Java contains classes that enable you to perform input and output of objects or variables of primitive data types. The data will still be stored as bytes or characters behind the scenes, allowing you to read or write data in the form of ints, Strings, or other types without having to worry about the details of converting such values to byte format. To perform such input and output, objects of classes ObjectInputStream and ObjectOutputStream can be used together with the byte-based file stream classes FileInputStream and FileOutputStream (these classes will be discussed in more detail shortly). The complete hierarchy of types in package java.io can be viewed in the online documentation at

```
download.oracle.com/javase/6/docs/api/java/io/package-tree.html
```

As you can see in the hierarchy, Java offers many classes for performing input/output operations. We use several of these classes in this chapter to implement file-processing programs that create and manipulate sequential-access files. In Chapter 27, we use stream classes extensively to implement networking applications.

In addition to the java.io classes, character-based input and output can be performed with classes Scanner and Formatter. Class Scanner is used extensively to input data from the keyboard—it can also read data from a file. Class Formatter enables formatted data to be output to any text-based stream in a manner similar to method System.out.printf. Appendix G presents the details of formatted output with printf. All these features can be used to format text files as well.

# 17.3 Class File

This section presents class File, which is useful for retrieving information about files or directories from disk. Objects of class File do not open files or provide any file-processing capabilities. However, File objects are used frequently with objects of other java.io classes to specify files or directories to manipulate.

# Creating File Objects

Class File provides four constructors. The one with a String argument specifies the name of a file or directory to associate with the File object. The name can contain path information as well as a file or directory name. A file or directory’s path specifies its location on disk. The path includes some or all of the directories leading to the file or directory. An absolute path contains all the directories, starting with the root directory, that lead to a specific file or directory. Every file or directory on a particular disk drive has the same root directory in its path. A relative path normally starts from the directory in which the application began executing and is therefore “relative” to the current directory. The constructor with two String arguments specifies an absolute or relative path as the first argument and the file or directory to associate with the File object as the second argument. The constructor with File and String arguments uses an existing File object that specifies the parent directory of the file or directory specified by the String argument. The fourth constructor uses a URI object to locate the file. A Uniform Resource Identifier (URI) is a more general form of the Uniform Resource Locators (URLs) that are used to locate websites. For example, http://www.deitel.com/ is the URL for the Deitel & Associates website. URIs for locating files vary across operating systems. On Windows platforms, the URI

```
file://C:/data.txt
```