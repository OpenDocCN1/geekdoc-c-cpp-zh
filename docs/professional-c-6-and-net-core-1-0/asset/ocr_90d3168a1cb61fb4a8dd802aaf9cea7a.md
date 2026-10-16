.MyDocuments to the GetFolderPath method. This feature of the Environment class is not available with .NET Core; thus in the following code the values of the environment variables HOMEDRIVE and HOMEPATH are used (code file WorkingWithFilesAndFolders/Program.cs):

```
private static string GetDocumentsFolder()
{
#if NET46    return
Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments).
#else    string drive =
Environment.GetEnvironmentVariable("HOMEDRIVE");    string path =
Environment.GetEnvironmentVariable("HOMEPATH");    return
Path.Combine(drive, path,"documents"); #endif

}
```

Environment.SpecialFolder is a huge enumeration that gives values for music, pictures, program files, app data, and many other folders.

# Creating Files and Folders

Now let’s get into using the File, FileInfo, Directory, and DirectoryInfo classes. First, the method CreateAFile creates the file Sample1.txt and adds the string Hello, World! to the file. An easy way to create a text file is to invoke the method WriteAllText of the File class. This method takes a filename and the string that should be written to the file. Everything is done with a single call (code file WorkingWithFilesAndFolders/Program.cs):

```
const string Sample1FileName ="Sample1.txt";
// etc.

public static void CreateAFile()
{
    string fileName = Path.Combine(GetDocumentsFolder(),
Sample1FileName);
    File.WriteAllText(fileName,"Hello, World!");
}
```

To copy a file, you can use either the Copy method of the File class or the CopyTo method of the FileInfo class:

```
var file = new FileInfo(@".\ReadMe.txt");
file.CopyTo(@"C:\Copies\ReadMe.txt");

File.Copy(@".\ReadMe.txt", @"C:\Copies\ReadMe.txt");
```

The first code snippet using FileInfo takes slightly longer to execute because of the need to instantiate an object named file, but it leaves file ready for you to perform further actions on the same file. When you use the second example, there is no need to instantiate an object to copy the file.

You can instantiate a FileInfo or DirectoryInfo class by passing to the constructor a string containing the path to the corresponding file system object. You have just seen the process for a file. For a folder, the code looks similar: