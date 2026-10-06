
## Using the File and Directory Classes

The File class contains methods that allow you to access information about files. Some of the methods are listed in Table 14-1.

| Method | Description |
| --- | --- |
| Create() | Creates a file |
| CreateText() | Creates a text file |
| Delete() | Deletes a file |
| Exists() | Returns true if the specified file exists |
| GetCreationTime() | Returns a DateTime object specifying when a file was created |
| GetLastWriteTime() | Returns a DateTime object specifying when a file was last modified |
| Move() | Moves a file to the specified location |

> DateTime is a structure that contains data about a date and time. In the chapter "Controls," you use the data from DateTime structures with MonthCalendar and DateTimePicker GUI objects. DateTime values can be expressed using Coordinated Universal Time (UTC), which is internationally recognized as Greenwich Mean Time (GMT). By default, DateTime values are expressed using the local time set on your computer. The property DateTime returns the current local time. The property DateTime.UtcNow returns the current UTC time.

The File class is contained in the System.IO namespace. So, to use the File class, you can use its fully qualified name, System.IO.File, or just use File if you include the statement using System.IO; at the top of your program file as shown in the first shaded statement in Figure 14-1.

14-1 shows a program that demonstrates several File class methods. The program prompts the user for a filename and then tests the file's existence in the second shaded statement. If the file does not exist, a message is displayed. Figure 14-2 shows two executions of the program. In the first execution, the user enters a filename that is not found. In the second execution, the file is found, the significant date and times are displayed.

> The System.IO.FileInfo class also allows you to access information about a file. See the Microsoft documentation at http://msn.microsoft.com for more information.

```csharp
using System.Console;
using System.IO;
class FileStatistics{
    static void Main()
    {
        string fileName;
        Write("Enter a filename >> ");
        fileName = ReadLine();
        if(File.Exists(fileName))
        {
            WriteLine("File exists");
            WriteLine("File was created " + 
                File.GetCreationTime(fileName));
            WriteLine("File was last written to " + 
                File.GetLastWriteTime(fileName));
        }
        else
        {
            WriteLine("File does not exist");
        }
    }
}
```

Figure 14-1 The FileStatistics program

In the FileStatistics program in Figure 14-1, the file must be in the same directory as the program that is running.

```
Enter a filename >> MyLetter.txt
File does not exist
```

```
Enter a filename >> BusinessLetter.txt
File exists
File was created 2/22/2017 8:09:46 AM
File was last written to 2/22/2017 8:38:24 AM
```

Figure 14-2 Two typical executions of the FileStatistics program

The Directory class provides you with information about directories or folders. Table 14-2 lists some available methods in the Directory class.

| Method | Description |
| --- | --- |
| CreateDirectory() | Creates a directory |
| Delete() | Deletes a directory |
| Exists() | Returns true if the specified directory exists |
| GetCreationTime() | Returns a DateTime object specifying when a directory was created |
| GetDirectories() | Returns a string that contains the names of the subdirectories |
| GetFiles() | Returns a string that contains the names of the files in the directory |
| GetLastWriteTime() | Returns a DateTime object specifying when a directory was last modified |
| Move() | Moves a directory to the specified location |

**Table 14-2** Selected Directory class methods

14-3 contains a program that declares an array of strings for filenames can be stored. (See the first shaded statement). The program prompts a user for a directory and then fills the string array with a list of filenames using the GetFiles() method. (See the second statement). Then a for loop is used to display the list of files. Figure 14-4 shows two typical executions of the program.

```csharp
using static System.Console;
using System.IO;
class DirectoryInformation
{
    static void Main()
    {
        string directoryName;
        string[] listFiles;
        Write("Enter a folder >> ");
        directoryName = ReadLine();
        if(Directory.Exists(directoryName))
        {
            WriteLine("Directory exists, " + 
                "and it contains the following: ");

            listFiles = Directory.GetFiles(directoryName);
            for(int x = 0; x < listFiles.Length; ++x)
                WriteLine("{0}", listFiles[x]);
        }
        else
        {
            WriteLine("Directory does not exist");
        }
    }
}
```

Figure 14-3 The DirectoryInformation program

```
Enter a folder >> ClientMemos
Directory exists, and it contains the following:
ClientMemos\ClientBillingWorksheet.xlsx
ClientMemos\JohnsonMemo.txt
ClientMemos\SmithMemo.txt
```

```
Enter a folder >> OtherMemos
Directory does not exist
```

Figure 14-4 Two typical executions of the DirectoryInformation program

Watch the video File Handling.

## Files and the File and Directory Classes

### TWO TRUTHS & A LIE
- 1. Temporary storage is nonvolatile; permanent storage is volatile.
- 2. When you write to a file, you copy data from RAM to a permanent storage device.
- 3. Most computer users organize their files into directories; the complete hierarchy of directories in which a file resides in its path.

> The false statement is #1. Temporary storage is volatile; permanent storage is nonvolatile.

## Understanding File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

The File class is contained in the System.IO namespace. So, to use the File class, you can use its fully qualified name, System.IO.File, or just use File if you include the statement using System.IO; at the top of your program file as shown in the first shaded statement in Figure 14-1.

14-1 shows a program that demonstrates several File class methods. The program prompts the user for a filename and then tests the file's existence in the second shaded statement. If the file does not exist, a message is displayed. Figure 14-2 shows two executions of the program. In the first execution, the user enters a filename that is not found. In the second execution, the file is found, the significant date and times are displayed.

> The System.IO.FileInfo class also allows you to access information about a file. See the Microsoft documentation at http://msn.microsoft.com for more information.

## Understanding File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an an is 011000001 or 01000001.

## File Data Organization

 data data data in a relationship the the the data,, the in in 114-... the,, the the the of the of the. the the.. a is of the the of the letters, numbers, or ( special symbols ( the the and and the the) that. data... the the the of bits ( the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.

## File Data Organization

Businesses store data in a relationship known as the data hierarchy, as described in Figure 14-5. For most users, the smallest piece of data is the character. A character is any one of the letters, numbers, or other special symbols (such as punctuation and arithmetic symbols) that constitute data. Characters are made up of bits (the zeros and ones that represent computer circuitry), but who use data do not care whether the internal representation for an A is 01000001 or 01000001.
