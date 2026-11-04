```
using (var watcher = new FileSystemWatcher(Path.GetTempPath(), "**.*"))
{
    watcher.Created += (o, e) =>
    {
        Console.WriteLine("Created: " + e.FullPath);
    };

    watcher.EnableRaisingEvents = true;

    Console.WriteLine("Monitoring... Press ENTER to exit.");
    Console.Read();
}
```

![](bbox=[0.07, 0.42, 0.48, 0.68])

FIGURE 28.2 Configuring an event handler for a FileSystemWatcher object.

To see the event handler getting called, opening an instance of Internet Explorer or an Office tool such as Word should do the trick because those programs write files to %TEMP%, using APIs similar to Path.GetTempFileName.

# Readers and Writers

At the heart of .NET's input/output model sits the concept of streams. Before we go there, let's look at the layer right above them. There we find the concept of readers (for the I in I/O) and writers (the O in I/O), both of which make use of streams easier. In fact, the file and directory APIs directly exposed those.

# The File Class

Alongside the FileInfo class, the System.IO namespace provides a home for a static class called File. Whereas one typically uses a FileInfo to pass around information about a file as an object, the File class provides a series of static methods that expose file system functionality. In fact, some of FileInfo's instance methods simply call into some of the static methods provided on file.