# Appendix B

# Command Line Development

An integrated development environment (IDE) like Visual Studio combines all the tools a developer needs into one comprehensive application. While this approach works well for most programmers, some developers prefer a less centralized approach, using instead command line tools to manage the development process. Command line tools are focused and fast, and each tool itself is fairly simple compared to a full-featured IDE. A developers may prefer a different editor to one provided by the IDE. Developers can build scripts to around command line tools to automate the building and testing process.

There are a few commands that are essential for working within the command-line environment. These center around manipulating and using files and folders. Our discussion assumes the Windows CMD.EXE shell, and we will note differences with macOS and Linux as needed. Linux and macOS are both Unix-like operating systems.

When you run CMD.EXE in Windows, the Terminal application on a Mac, or a bash terminal in Linux, the operating system presents a text-based console window. You type commands into this window and receive text feedback. Most of the commands are programs that you launch by typing their name. The following lists common commands useful for using the command-line;

+   • dir
+   
+   When the command line interface starts it locates you in a particular folder, or directory, in the file system managed by the operating system. Your location is known as the current working directory. The command dir prints a list of the files in your current working directory. On Unix-like machine the ls -l command performs similar work. The command dir /w displays a wide listing of the files with fewer details; the ls command is the equivalent on Unix-like systems.

+   • mkdir name
+   
+   Creates a new subdirectory (subfolder) named name in the current directory. Subdirectories allow you to better organize your files.

+   • cd name
+   
+   Changes you current directory to be that specified by name. Some examples of its use include
+   
+   - cd Code
+   
+   Changes the current working directory to be the subdirectory named Code. Here the name is relative to the current directory. It is an error to provide a name that does not correspond to a subdirectory of the current directory.