```
File.FullName, FileMode.OpenOrCreate,
 FileAccess.ReadWrite);
 }
```

```
// Finalizer
 ~TemporaryFileStream()
 {
 Close();
 }
```

```
public FileStream Stream
 {
 get { return _Stream; }
 }
 readonly private FileStream _Stream;
```

```
public FileInfo File
 {
 get { return _File; }
 }
 readonly private FileInfo _File =
 new FileInfo(Path.GetTempFileName()));
```

```
public void Close()
 {
 if(Stream != null)
 {
 Stream.Close();
 }
 if(File != null)
 {
 File.Delete();
 }
 }
 }
```

Finalizers do not allow any parameters to be passed, and as a result, finalizers cannot be overloaded. Furthermore, finalizers cannot be called explicitly. Only the garbage collector can invoke a finalizer. Therefore, access modifiers on finalizers are meaningless, and as such, they are not supported. Finalizers in base classes will be invoked automatically as part of an object finalization call.

Because the garbage collector handles all memory management, finalizers are not responsible for de-allocating memory. Rather, they are responsible for freeing up resources such as database connections and file