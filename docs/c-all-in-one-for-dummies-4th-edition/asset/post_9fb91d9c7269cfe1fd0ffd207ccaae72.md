
You can see how main() follows the previously outlined steps. Each data structure uses its own function called DumpEntry(). The DumpEntry() function prints the file information. Here's what you should see when you run the application (the current directory entry, the parent directory entry, and directories containing the examples for this chapter; your list may vary slightly):

```text
Sun Jul 26 15:04:54 2020   0    [.]
Sun Jul 26 15:04:54 2020   0    [..]
Sun Jul 26 16:12:09 2020   0    [DeleteDirectory]
Sun Jul 26 15:04:51 2020   0    [FileSystem]
Sun Jul 26 16:24:47 2020   0    [GetDirectoryContents]
Sun Jul 26 16:03:32 2020   0    [MakeDirectory]
```

The DumpEntry() function tests whether the item is a directory. This is another old (but reliable) way to program: You check for the presence of a particular bit in the middle of the attrib member of the structure, like this:

```cpp
if ((data.attrib & _A_SUBDIR) == _A_SUBDIR)
    cout << "[" << data.name << "]" << endl;
else
    cout << data.name << endl;
```

The Chop() function removes an extraneous carriage return that the ctime() function adds to the end of the string it creates. Otherwise, the information after the date has to start on the next line of text, which isn't what the example needs.

## Copying Files

When you copy a file from one location to another, you actually create a new file and fill it with the same contents as the original file. To perform this task, you have to read each byte from the first file and write it to the second. To make matters worse, copying a file means you have to make sure that you copy it exactly the same, that you don't accidentally tack an extra 0 or two at the end of the file, or an extra carriage return or linefeed at the end of the file (which could happen when you copy a text file). The two files should be identical — not only contain the same information, but also be the same size.

These are the basics, but most good copy routines do more. They give the new file a date that matches the date of the original file, and they set all the attributes, such as read-only, the same. There are a few ways to perform a copying task, but the following sections provide two of them.

### Copying with Windows

If you’re programming in Windows, you can use an easy method to perform copying tasks: the CopyFile function. To use it, you include the line `#include <windows.h>` in your application. Then you just do the following:

```cpp
CopyFile("c:/dog.txt", "c:/dog2.txt", TRUE);
```

This code copies from `c:/dog.txt` to `c:/dog2.txt`. The final parameter, TRUE in all capitals, is a preprocessor macro defined somewhere in the bowels of the Windows header files. You have to use either TRUE or FALSE when calling any of the Windows functions. When the early versions of Windows were around, no bool type existed, so resourceful developers defined their own TRUE and FALSE as integers. That final parameter in CopyFile() tells the function what to do if the file you’re copying to already exists: TRUE means don’t overwrite the existing file; just abort. FALSE means overwrite it.

### Using the quick-and-dirty method

There’s another way you can copy a file, and you can use this to also move, delete, and rename files. However, this method isn’t portable: The code is operating-system specific, which means that a Windows application won’t run on Linux and vice versa. You can execute any DOS or Unix-shell commands by using the system() function. For example, this code pauses the display:

```cpp
system("PAUSE");
```

This code runs the pause command, which prints the message

```text
Press any key to continue . . .
```

and waits for you to press a key. Because the `system()` function can run any shell command, you can use it to call the copy command, like this:

```cpp
system("copy c:\\abc.txt c:\\def.txt");
```

Note that the command uses the backslash, not a forward slash due to limitations in the Windows command processor. If you’re using some other platform, you need to consider the needs of the platform when formatting commands.

## Moving and Renaming Files and Directories

You may have a file called

```text
dog1.txt
```

and need to rename it to

```text
temp\dog1.txt
```

This doesn't look like a valid way to rename a file. Notice that the file started out being called dog1.txt, and afterward it's still called dog1.txt. Rather than being renamed, the file appears to have moved to a new location — the temp subdirectory. The reason this is called a rename is that the file's real name is the entire pathname and filename together. For this reason, you can move and rename both files and directories using the same function. Of course, the path must exist. If you try to rename `c:\dog1.txt` to `c:\temp\dog1.txt` and there's no `c:\temp` directory, the rename fails and you get an error message.

The RenameFile example renames a file. Note that you must create a dog1.txt file and a temp directory in the `\CPP_AIO4\BookVI\Chapter04\RenameFile` folder for this example to work.

```cpp
#include <iostream>
#include <stdio.h>

using namespace std;

int main() {
    if (rename("dog1.txt", "dog2.txt") == 0)
        cout << "Renaming dog1.txt to dog2.txt." << endl;

    if (rename("dog2.txt", "dog1.txt") == 0)
        cout << "Renaming dog2.txt to dog1.txt." << endl;

    if (rename("dog1.txt", "temp/dog2.txt") == 0)
        cout << "Renaming dog1.txt to temp/dog2.txt." << endl;

    if (rename("temp/dog2.txt", "dog1.txt") == 0)
        cout << "Getting back to start with dog1.txt."
             << endl;

    return 0;
}
```

The example uses the `rename()` function, passing first the old filename and then the new filename. The first call renames the file from dog1.txt to dog2.txt. The second call renames it from dog2.txt to dog1.txt. Finally, the code moves the file to the temp directory, but only if you created it. When you run this example, you see the following output:

```text
Renaming dog1.txt to dog2.txt.
Renaming dog2.txt to dog1.txt.
Renaming dog1.txt to temp/dog2.txt.
Getting back to start with dog1.txt.
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_755_0.png)

You can also give the file a new filename when you move it, as in this code:

```cpp
rename("dog1.txt", "temp/cat.txt");
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_755_1.png)

There are conditions under which the rename operation won't work:

- You're renaming the file to move it to a new directory, but that directory does not exist. In this case, create the directory before you move the file.
- You're renaming a file but some other file in the current directory already exists under that name. In this case, either delete the other file or (better yet) make your application ask its users what they want it to do: Delete the old file (that is, "overwrite it")? Abort the operation?
- You're renaming a file to move it to a new directory, but there's already a file by that name in that directory. In this case, as in the previous example, get your application to ask the users what to do — overwrite or abort?
- The file is locked by another application, such as when you open the file for editing.

![](img/128ab511de4e7360e167e3b15cdd5dd0_755_2.png)

Renaming also works with directories. You can move directory names around just as if they were files. But there's a catch: If any application has a file open within that directory, the `rename()` function won't work. The operating system lets you move or rename a directory only if you're not accessing any files inside the directory.

## Chapter 5: Streaming Your Own Classes

The C++ stream classes can read and write all sorts of goodies, such as integers, characters, strings, floating-point numbers, and Boolean variables. But sooner or later, being able to stream one of your own classes (like the following) would be nice:

```cpp
MyClass x;
cout << x << endl;
```

C++ has a good reason not to have done this already: The compiler and library can't predict on their own how you want to stream your class using cout. (The example in the "Writing and reading structured data" section of Chapter 3 of this minibook shows one technique for accomplishing this task by overriding the `<<` operator.) Here are some examples:

- The name of the class followed by the values of the public properties.
- The private properties.
- Derived values or some other information related to the class.
