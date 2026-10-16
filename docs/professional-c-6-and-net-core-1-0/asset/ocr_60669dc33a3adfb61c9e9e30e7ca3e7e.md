The shared memory can be bigger than the available physical memory, so a backing store is needed. You can create a memory mapped file to a specific file or shared memory. With either of these options, you can assign a name for the memory map. Using a name allows different processes to have access to the same shared memory.

After you’ve created the memory map, you can create a view. A view is used to map a part of the complete memory mapped file to access it for reading or writing.

The MemoryMappedFilesSample makes use of the following dependencies and namespaces:

# Dependencies

```
NETStandard.Library

System.IO.MemoryMappedFiles
```

# Namespaces

```
System

System.IO

System.IO.MemoryMappedFiles

System.Threading

System.Threading.Tasks

static System.Console
```

The sample application demonstrates using a memory mapped file using both view accessors and streams using multiple tasks. One task creates the memory mapped file and writes data to it; the other task reads data.

> NOTE The sample code makes use of tasks and events. Read Chapter 21, “Tasks and Parallel Programming,” for more information about tasks, and Chapter 22, “Task Synchronization,” for more information about events.

Some infrastructure is needed for creating the tasks and signaling when the map is ready and the data is written. The name of the map and ManualResetEventSlim objects are defined as a member of the Program class (code file MemoryMappedFilesSample/Program.cs):

```
private ManualResetEventSlim _mapCreated =
    new ManualResetEventSlim(initialState: false);
private ManualResetEventSlim _dataWrittenEvent =
    new ManualResetEventSlim(initialState: false);
private const string MAPNAME ="SampleMap";
```

Tasks are started within the Main method with the Task.Run method:

```
public void Run()
{
    Task.Run(() => WriterAsync());
```