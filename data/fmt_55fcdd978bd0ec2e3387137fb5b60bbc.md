
要创建 ZIP 归档，您可以创建 `ZipArchive` 对象。`ZipArchive` 包含多个 `ZipArchiveEntry` 对象。`ZipArchive` 类不是流，但它使用流进行读写（这与前面讨论的读写器类类似）。以下代码片段创建一个 `ZipArchive`，将压缩内容写入使用 `File.OpenWrite` 打开的文件流。添加到 ZIP 归档的内容由传递的目录定义。`Directory.EnumerateFiles` 枚举目录中的所有文件，并为每个文件创建一个 `ZipArchiveEntry` 对象。调用 `Open` 方法会创建一个 `Stream` 对象。通过读取流的 `CopyTo` 方法，文件会被压缩并写入 `ZipArchiveEntry`（代码文件 `CompressFileSample/Program.cs`）：

```csharp
public static void CreateZipFile(string directory, string zipFile)
{
    FileStream zipStream = File.OpenWrite(zipFile);

    using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create))
    {
        IEnumerable<string> files = Directory.EnumerateFiles(
            directory, "*", SearchOption.TopDirectoryOnly);

        foreach (var file in files)
        {
            // code cut off in image
        }
    }
}

ZipArchiveEntry entry =
archive.CreateEntry(Path.GetFileName(file));
using (FileStream inputStream = File.OpenRead(file))
using (Stream outputStream = entry.Open())
{
    inputStream.CopyTo(outputStream);
}
}
}
```

### 监视文件更改

使用 `FileSystemWatcher`，您可以监视文件更改。创建、重命名、删除和更改文件时都会触发事件。这可用于需要对文件更改做出反应的场景——例如，当文件上传到服务器时，或在文件缓存在内存中且文件更改时需要使缓存失效的情况下。

由于 `FileSystemWatcher` 易于使用，让我们直接进入示例。`FileMonitor` 的示例代码使用了以下依赖项和命名空间：

#### Dependencies

```
NETStandard.Library

System.IO.FileSystem.Watcher
```

#### Namespaces

```
System.IO

static System.Console
```

示例代码在方法 `WatchFiles` 中开始监视文件。使用 `FileSystemWatcher` 的构造函数，您可以提供应被监视的目录。您还可以提供过滤器以仅过滤与过滤器表达式匹配的特定文件。当您设置 `IncludeSubdirectories` 属性时，您可以定义是否只应监视指定目录中的文件，或者是否也应监视子目录中的文件。通过 `Created`、`Changed`、`Deleted` 和 `Renamed` 事件，提供事件处理程序。所有这些事件的类型都是 `FileSystemEventHandler`，`Renamed` 事件除外，其类型为 `RenamedEventHandler`。`RenamedEventHandler` 派生自 `FileSystemEventHandler` 并提供有关事件的附加信息（代码文件 `FileMonitor/Program.cs`）：

```csharp
public static void WatchFiles(string path, string filter)
{
    var watcher = new FileSystemWatcher(path, filter)
    {
        IncludeSubdirectories = true
    };
    watcher.Created += OnFileChanged;
    watcher.Changed += OnFileChanged;
    watcher.Deleted += OnFileChanged;

    watcher.Renamed += OnFileRenamed;

    watcher.EnableRaisingEvents = true;
    WriteLine("watching file changes...");
}
```

文件更改时接收到的信息类型为 `FileSystemEventArgs`。它包含更改的文件名称以及更改类型，该类型是 `WatcherChangeTypes` 类型的枚举：

```csharp
private static void OnFileChanged(object sender,
FileSystemEventArgs e)
{
    WriteLine($"file {e.Name} {e.ChangeType}");
}
```

重命名文件时，会通过 `RenamedEventArgs` 参数接收附加信息。此类型派生自 `FileSystemEventArgs`，并定义了有关文件原始名称的附加信息：

```csharp
private static void OnFileRenamed(object sender,
RenamedEventArgs e)
{
    WriteLine($"file {e.OldName} {e.ChangeType} to {e.Name}");
}
```

当你通过指定要监视的文件夹和 `*.txt` 作为筛选器来启动应用程序时，以下是创建文件 `sample1.txt`、添加内容、将其重命名为 `sample2.txt` 并最终删除后的输出：

```
watching file changes...
file New Text Document.txt Created
file New Text Document.txt Renamed to sample1.txt
file sample1.txt Changed
file sample1.txt Changed
file sample1.txt Renamed to sample2.txt
file sample2.txt Deleted
```

### 使用内存映射文件

内存映射文件使您能够从不同进程访问文件或共享内存。此技术有几种应用场景和功能：

- 使用文件映射快速随机访问大文件
- 在不同进程或任务之间共享文件
- 在不同进程或任务之间共享内存
- 使用访问器直接读写内存位置
- 使用流进行读写

内存映射文件 API 允许您使用物理文件或共享内存——其中系统页面文件用作后备存储。

共享内存可能大于可用物理内存，因此需要后备存储。您可以针对特定文件或共享内存创建内存映射文件。使用这两种选项中的任何一种，您都可以为内存映射指定名称。使用名称可以使不同进程访问同一共享内存。

创建内存映射后，您可以创建视图。视图用于映射完整内存映射文件的一部分，以便对其进行读取或写入访问。

`MemoryMappedFilesSample` 使用了以下依赖项和命名空间：

#### 依赖项

```
NETStandard.Library

System.IO.MemoryMappedFiles
```

#### 命名空间

```
System

System.IO

System.IO.MemoryMappedFiles

System.Threading

System.Threading.Tasks

static System.Console
```

示例应用程序演示了如何使用视图访问器和流，通过多个任务使用内存映射文件。一个任务创建内存映射文件并向其写入数据；另一个任务读取数据。

> 注意 示例代码使用了任务和事件。有关任务的更多信息，请参阅第 21 章“任务与并行编程”；有关事件的更多信息，请参阅第 22 章“任务同步”。

创建任务以及在地图就绪和数据写入时发出信号需要一些基础结构。地图的名称和 `ManualResetEventSlim` 对象被定义为 `Program` 类的成员（代码文件 `MemoryMappedFilesSample/Program.cs`）：

```csharp
private ManualResetEventSlim _mapCreated =
    new ManualResetEventSlim(initialState: false);
private ManualResetEventSlim _dataWrittenEvent =
    new ManualResetEventSlim(initialState: false);
private const string MAPNAME ="SampleMap";
```

任务在 `Main` 方法中使用 `Task.Run` 方法启动：

```csharp
public void Run()
{
    Task.Run(() => WriterAsync());

    Task.Run(() => Reader());
    WriteLine("tasks started");
    ReadLine();
}
```

### 使用访问器创建内存映射文件

要创建基于内存的内存映射文件，写入方调用 `MemoryMappedFile.CreateOrOpen` 方法。此方法要么打开第一个参数指定名称的对象，要么在对象不存在时创建一个新对象。要打开现有文件，可以使用 `OpenExisting` 方法。要访问物理文件，可以使用 `CreateFromFile` 方法。

示例代码中使用的其他参数是内存映射文件的大小和所需的访问权限。创建内存映射文件后，会发出 `_mapCreated` 事件，以告知其他任务内存映射文件已创建并可打开。调用 `CreateViewAccessor` 方法会返回一个 `MemoryMappedViewAccessor` 以访问共享内存。使用视图访问器，您可以定义此任务使用的偏移量和大小。当然，您可以使用的最大大小是内存映射文件本身的大小。此视图用于写入，因此文件访问设置为 `MemoryMappedFileAccess.Write`。

接下来，您可以使用 `MemoryMappedViewAccessor` 的重载 `Write` 方法将原始数据类型写入共享内存。`Write` 方法始终需要位置信息来指定数据应写入的位置。所有数据写入后，会发出一个事件通知读取方现在可以开始读取（代码文件 `MemoryMappedFilesSample/Program.cs`）：

```csharp
private async Task WriterAsync()
{
    try
    {
        using (MemoryMappedFile mappedFile =
MemoryMappedFile.CreateOrOpen(
            MAPNAME, 10000, MemoryMappedFileAccess.ReadWrite))
        {
            _mapCreated.Set(); // signal shared memory segment created
            WriteLine("shared memory segment created");

            using (MemoryMappedViewAccessor accessor =
mappedFile.CreateViewAccessor(
                0, 10000, MemoryMappedFileAccess.Write))
            {
                for (int i = 0, pos = 0; i < 100; i++, pos += 4)
                {
                    accessor.Write(pos, i);
                    WriteLine($"written {i} at position {pos}");
                    await Task.Delay(10);
                }
            }
            _dataWrittenEvent.Set(); // signal all data written
            WriteLine("data written");
        }
    }
    catch (Exception ex)
    {
        WriteLine($"writer {ex.Message}");
    }
}

private void Reader()
{
    try
    {
        WriteLine("reader");

        _mapCreated.Wait();

        WriteLine("reader starting");

        using (MemoryMappedFile mappedFile =
            MemoryMappedFile.OpenExisting(
                MAPNAME, MemoryMappedFileRights.Read))
        {
            using (MemoryMappedViewAccessor accessor =
                mappedFile.CreateViewAccessor(
                    0, 10000, MemoryMappedFileAccess.Read))
            {
                _dataWrittenEvent.Wait();

                WriteLine("reading can start now");

                for (int i = 0; i < 400; i += 4)
                {
                    int result = accessor.ReadInt32(i);
                    WriteLine($"reading {result} from position {i}");
                }
            }
        }
    }
    catch (Exception ex)
    {
        WriteLine($"reader {ex.Message}");
    }
}
```

读取方首先等待地图创建完成，然后使用 `MemoryMappedFile.OpenExisting` 打开内存映射文件。读取方只需要对地图的读取访问权限。之后，与之前的写入方类似，创建一个视图访问器。在读取数据之前，需要等待 `_dataWrittenEvent` 被设置。读取与写入类似，需要提供数据访问的位置，但定义了不同的 `Read` 方法（如 `ReadInt32`）来读取不同的数据类型：

运行应用程序时，您可能会看到类似以下的输出：

```
reader

reader starting

tasks started

shared memory segment created

written 0 at position 0

written 1 at position 4

written 2 at position 8

...

written 99 at 396
```
