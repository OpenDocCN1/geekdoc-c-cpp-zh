Being able to manually modify these properties might seem strange at first, but it can be quite useful. For example, if you have a program that effectively modifies a file by simply reading it in, deleting it, and creating a new file with the new contents, you would probably want to modify the creation date to match the original creation date of the old file.

# The Path Class

The Path class is not a class that you would instantiate. Rather, it exposes some static methods that make operations on pathnames easier. For example, suppose that you want to display the full pathname for a file, ReadMe.txt, in the folder C:\My Documents. You could find the path to the file using the following code:

```
Console.WriteLine(Path.Combine(@"C:\My Documents\", "ReadMe.txt"));
```

Using the Path class is a lot easier than using separation symbols manually, especially because the Path class is aware of different formats for pathnames on different operating systems. At the time of this writing, Windows is the only operating system supported by .NET. However, if .NET is ported to UNIX, Path would be able to cope with UNIX paths, in which case / , rather than \, would be used as a separator in pathnames. Path.Combine() is the method of this class that you are likely to use most often, but Path also implements other methods that supply information about the path or the required format for it.

Some of the static fields available to the Path class include the following:

| PROPERTY | DESCRIPTION |
|---|---|
| AltDirectorySeparatorChar | Provides a platform-agnostic way to specify an alternative character to separate directory levels. In Windows, a / symbol is used, whereas in UNIX, a \ symbol is used. |
| DirectorySeparatorChar | Provides a platform-agnostic way to specify a character to separate directory levels. In Windows, a \ symbol is used, whereas in UNIX, a / symbol is used. |
| PathSeparator | Provides a platform-agnostic way to specify path strings which divide environmental variables. The default value of this setting is a semicolon. |
| VolumeSeparatorChar | Provides a platform-agnostic way to specify a volume separator. The default value of this setting is a colon. |

The following example illustrates how to browse directories and view the properties of files.

# A FileProperties Sample

This section presents a sample C# application called FileProperties. This application presents a simple user interface that allows you to browse the file system and view the creation time, last access time, last write time, and size of files. (You can download the sample code for this application from the Wrox web site at www.wrox.com.)

The FileProperties application works like this. You type in the name of a folder or file in the main text box at the top of the window and click the Display button. If you type in the path to a folder, its contents are listed in the list boxes. If you type in the path to a file, its details are displayed in the text boxes at the bottom of the form and the contents of its parent folder are displayed in the list boxes. Figure 29-2 shows the FileProperties sample application in action.

The user can very easily navigate around the file system by clicking any folder in the right-hand list box to move down to that folder or by clicking the Up button to move up to the parent folder. Figure 29-2 shows the contents of my User folder. The user can also select a file by clicking its name in the list box. This displays the file's properties in the text boxes at the bottom of the application (see Figure 29-3).