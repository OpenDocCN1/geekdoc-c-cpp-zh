The methods provided by NSFHandle can also be applied to devices or sockets. However, we will focus only on dealing with ordinary files in this chapter.

The NSURL class allows you to work with URLs in your applications. We'll take a look at this class with a simple example that shows how you can read data from the Internet.

The NSBundle class provides methods that allow you to work with your application's bundle. This includes the ability to search the bundle for specific resources, for example all JPEG images. We'll touch on this class lightly towards the end of the chapter.

# Managing Files and Directories: NSFileManager

A file or directory is uniquely identified by NSFileManager using a pathname to the file. A pathname is an NSString object that can either be a relative or full pathname. A relative pathname is one that is relative to the current directory. So, the filename copy1.m would mean the file copy1.m in the current directory. Slash characters separate a list of directories in a path. The filename ch16/copy1.m is also a relative pathname, identifying the file copy1.m stored in the directory ch16, which is contained in the current directory.

Full pathnames, also known as absolute pathnames, begin with a leading /. Slash is actually a directory, called the root directory. On my Mac, the full pathname to my home directory is /Users/stevekochan. This pathname specifies three directories: / (the root directory), Users, and stevekochan.

The special tilde character (-) is used as an abbreviation for a user's home directory. ~linda would, therefore, be an abbreviation for the user linda home directory, which might be the path /Users/linda. A solitary tilde character indicates the current user's home directory, meaning the pathname ~/copy1.m would