```
{
    Console.WriteLine("File created: " + e.FullPath);
}

static void fileWatcher_Changed(object sender, FileSystemEventArgs e)
{
    Console.WriteLine("File changed: " + e.FullPath);
}

static void fileWatcher_Renamed(object sender, RenamedEventArgs e)
{
    Console.WriteLine("File renamed: " + e.FullPath);
}

static void fileWatcher_Deleted(object sender, FileSystemEventArgs e)
{
    Console.WriteLine("File deleted: " + e.FullPath);
}
}
```

You first create an instance of the FileSystemWatcher class by initializing its Path and Filter properties:

```
FileSystemWatcher fileWatcher = new FileSystemWatcher()
{
    Path = @"C:\",
    Filter = "*.txt"
};
```

Here, you are monitoring the C:\ drive and all its files ending with the .txt extension.

You then wire all the events with their respective event handlers:

```
//---wire up the event handlers---
fileWatcher.Deleted += new FileSystemEventHandler(fileWatcher_Deleted);
fileWatcher.Renamed += new RenamedEventHandler(fileWatcher_Renamed);
fileWatcher.Changed += new FileSystemEventHandler(fileWatcher_Changed);
fileWatcher.Created += new FileSystemEventHandler(fileWatcher_Created);
```

These statements handle four events:

+   - Deleted — Fires when a file is deleted
+   - Renamed — Fires when a file is renamed
+   - Changed — Fires when a file's content is changed
+   - Created — Fires when a file is created