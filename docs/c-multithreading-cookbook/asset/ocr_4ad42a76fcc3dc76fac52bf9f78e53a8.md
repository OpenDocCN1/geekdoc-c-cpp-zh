# What you need for this book

Execute the examples in the book, the following software will be required:

+   - Visual Studio 2013
  - http://www.visualstudio.com/downloads/download-visual-studio-vsd-express-windows-8
- Windows Drivers Kit: WinDDK
  - http://msdn.microsoft.com/en-us/windows/hardware/hb852365.aspx
- MySQL Connector C
  - http://dev.mysql.com/downloads/connector/c/

# Who is this book for

This book is intended primarily for intermediate and advanced users. Synchronization concepts are conceived from the very beginning, thus making the book readable for all developers unassociated to any particular branch of expertise. The last two chapters will provide great knowledge to advanced users, providing an excellent overview on concepts such as concurrent design and advanced thread management.

# Conventions

In this book, you will find a number of styles of text that distinguish between different kinds of information. Here are some examples of these styles, and an explanation of their meaning.

Code words in text, database table names, folder names, filenames, file extensions, pathnames, dummy URLs, user input, and Twitter handles are shown as follows: "We can include other contexts through the use of the `include` directive."

A block of code is set as follows:

```
class CLock
{
  public:
    CLOCK(TCHAR* szMutexName);
    -CLock();
```