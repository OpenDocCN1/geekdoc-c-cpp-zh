don't work if the user doesn't have a C: drive or is using another operating system. Relative paths have a similar but less obvious problem.

```
./relative/path/to/file.txt
```

Using a relative file path works if the Java application is launched in the correct folder, but can break if the application is started from another location. For example, creating a script that launches the program from another directory will break the relative path. Although it is acceptable to allow the users to start the application only from the current directory, there is an easier way.

Most people who have used Java for a while are familiar with the classpath; that magical list of all the directories and JAR files needed to run the application. Not only can you add JAR files and folders to the classpath, but you can access JAR files and folders with resources. When you include resources in the classpath, it doesn't matter where the application is launched. Paths to the files are the same on any file system in any operating system.

Before you get too excited, it is important to understand some weird differences between the different methods of opening classpath resources. There are two different classes that can be used to load resources from the classpath.

+   - ClassLoader.getSystemResourceAsStream()
+   - Class.getResourceAsStream()

These two methods look very similar, so it is easy to confuse them. Because they are almost, but not quite, the same, you must be careful to ensure the correct resource is given to the correct method.

Here is where the confusing part comes into play. Both ClassLoader and Class can load resources with an absolute path, but only Class can load relative resources. See Figure 9.2.

| | Absolute | Relative |
|---|---|---|
| ClassLoader | ☑ | |
| Class | ☑ | ☑ |

Figure 9.2
Class Loader Resources.
© 2014 Timothy Wright.