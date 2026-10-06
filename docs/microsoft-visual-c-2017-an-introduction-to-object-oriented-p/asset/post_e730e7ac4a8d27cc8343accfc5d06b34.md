
To write to a file is to store data in a computer file on a permanent storage device.

Persistent storage is nonvolatile storage.

The root directory is the main directory of a storage device.

Folders or directories are structures to organize files on a storage device.

A path is composed of the disk drive in which a file resides plus the complete hierarchy of directories.

The data hierarchy is the relationship of characters, fields, records, and files.

A character is any of the letters, numbers, or other special symbols (such as punctuation marks) that constitute data.

A character set is the group of all characters used to represent data on a particular computer.

A field is a character or group of characters that has some meaning.

A record is a collection of files that contain data about an entity.

A sequential access file is a data file in which each record is read in order based on its position in the file; usually the records are stored in order based on the value in some field.

The key field is the field used to control the order of records in a sequential file.

A random access file is one for which records can be accessed in any order.

Opening a file means creating an object and associating a stream of bytes with it.

Closing a file means it is no longer available to an application.

A stream is a pipeline or channel through which bytes are input from and output to a file. Programmers say FileStream exposes a stream around a file.

XML is an abbreviation of Extensible Markup Language, which is a standard for exchanging data over the Internet.

A token is a block of text within a string that represents an entity or field.

A delimiter is a character used to specify the boundary between characters in text files.

A CSV file is one that contains comma-separated values.

A priming read is an input statement that gets a first data item or record.

The term magic number refers to the bad programming of hard-coding numbers in code without explanation.

A file position pointer holds the number of the next byte to be read.

Serialization is the process of converting objects into streams of bytes.

Deserialization is the process of converting streams of bytes back into objects.

## Review Questions

- 1. Random access memory is
a. volatile permanent
b. persistent
d. sequential

- 2. A collection of data stored on a nonvolatile device in a computer system is a(n)
a. application computer file
b. operating system
memory map

- 3. Which of the following is not considered to be permanent storage?
a. a USB drive
b. a hard drive
c. RAM
d. None of these is permanent storage.

- 4. When you store data in a computer file on a persistent storage device, you are
a. reading
b. writing
d. rooting

- 5. Which of the following is not a File class method?
a. Create() Exists()
b. Delete()
d. End()

- 6. In the data hierarchy, a group of characters that has some meaning, such as a last name or ID number, is a
a. byte file
b. field
d. record

- 7. When each record in a file is stored in order based on the value in some field, the file is a(n) file.
a. random access formatted
b. sequential application

- 8. A channel through which data flows between a program and storage is a
a. path
c. directory
b. folder
d. stream

- 9. Which of the following is not part of a FileStream constructor?
a. the file size
c. the filename
b. the file mode
d. the type of access

- 10. When a file's mode is Create, a new file will be created
a. even if one with the same name already exists
b. only if one with the same name does not already exist
c. only if one with the same name already exists
d. only if the access is Read

- 11. Which of the following is not a FileStream property?
a. CanRead
c. CanSeek
b. CanExists
d. CanWrite

- 12. Which of the following is not a file Access enumeration?
a. Read
c. WriteRead
b. Write
d. ReadWrite

- 13. A character used to specify the boundary between data items in text files is a
a. sentinel
c. delimiter
b. stopgap
d. margin

- 14. Which character can be used to specify a boundary between characters in text files?
a. a comma
c. either of these
b. a semicolon
d. neither of these

- 15. After a StreamReader has been created, the ReadLine() method can be used to
a. retrieve one line at a time from the file
b. retrieve one character at a time from the file
c. store one line at a time in a file
d. split a string into tokens

- 16. The argument to the String class Split() method is ____________________.
a. void
b. the number of fields into which to split a record
c. the character that identifies a new field in a string
d. a string that can be split into tokens

- 17. The String class Split() method stores its results in ____________________.
a. a string
b. an array of strings
c. an appropriate data type for each token
d. an array of bytes

- 18. A file's ____________________ holds the byte number of the next byte to be read.
a. index indicator
c. header field
b. position pointer
d. key field

- 19. The process of converting objects into streams of bytes is
a. mapping
b. splitting
d. serialization

- 20. Which of the following is serializable?
a. an int
b. a string
c. an array of ints
d. all of above

## CHAPTER 14 Files and Streams

### Programming Exercises

- 1. Create a program named DirectoryInformation that allows the user to enter names. If the directory exists, list the files; otherwise, display a message indicating the directory does not exist. Create as many as necessary.

- 2. Create a program named FileComparison that compares two files. First, use a text editor as Notepad to save the files. Next, display the size. Use a System.IO.FileInfo object using the following:
```csharp
FileInfo fileInfo = new FileInfo(fileName);
size = fileInfo.Length;
```

- 3. Create a program named CustomizeForm that includes a Form for which the user can select options for the background color, size, and title. Change each feature of the Form as the user makes selections. After the user clicks a button to save the form settings, save the color, size, and title as strings to a file, and disable the button.

- 4. Design a program named RetrieveCustomizedForm that includes a Form with a Button. When the user clicks the Button, the retrieved saved to the file in the CustomizeForm project in Exercise 5 are retrieved, and the new Form's color, size, and title are set appropriately.

- 5. Create a program named highScore containing a Form that hosts a game in which the computer randomly selects one of three letters (A, B, or C) and the user tries to guess which letter was selected. At the start of the game, read the previous high score from a data file. (Create this file to hold 0) Display the previous high score on the Form to show the player the score to try to beat. Play continues for 10 rounds. As the player makes each guess, show the player's guess and the computer's choice, and award a point if the player correctly guesses the computer's choice. Keep a running count of the number of correct guesses. After 10 rounds, disable the game controls, and create a file that holds the new high score, which might be the same as before or a higher number.
