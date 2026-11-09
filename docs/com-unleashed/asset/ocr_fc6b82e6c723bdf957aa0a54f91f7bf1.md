| **TABLE 4.2** | **The IPersistStreamInit Interface** |
|---|---|
| **Method** | **Description** |
| `QueryInterface` | Inherited from IUnknown |
| `AddRef` | Inherited from IUnknown |
| `Release` | Inherited from IUnknown |
| `GetClassID` | Inherited from IPersist |
| `IsDirty` | Checks the object for changes since it was last saved |
| `Load` | Initializes an object from the stream where it was previously saved |
| `Save` | Saves an object into the specified stream and indicates whether the object should reset its dirty flag |
| `GetSizeMax` | Returns the size in bytes of the stream needed to save the object |
| `InitNew` | Initializes the object to a default state |

# The `IStream` Interface

The `IStream` interface supports reading and writing data to stream objects. Stream objects contain data in a structured storage object. Simple data can be written directly to a stream, but most frequently, streams are elements nested within a storage object. They are similar to standard files.

The `IStream` interface defines methods similar to the MS-DOS file functions. For example, each stream object has its own access rights and a seek pointer. The main difference between a stream object and a DOS file is that streams are not opened using a file handle, but through an `IStream` interface pointer.

The methods in this interface present your object's data as a contiguous sequence of bytes that you can read or write. There are also methods for committing and reverting changes on streams open in transacted mode and methods for restricting access to a range of bytes in the stream.

Streams can remain open for long periods of time without consuming file system resources. The `IStream::Release` method is similar to a close function on a file. Once it is released, the stream object is no longer valid and cannot be used.

Table 4.2 shows the `IStream` methods and gives a short description of each.