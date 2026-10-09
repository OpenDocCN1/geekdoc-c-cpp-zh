```
public void Save()
{
 DataStorage.Store(this);
}
```

```
class DataStorage
{
 // Save an employee object to a file
 // named with the Employee name
 public static void Store(Employee employee)
 { // ...
}
```

The Save() method in Listing 6.12 calls a method on the DataStorage class, called Store(). The Store() method, however, needs to be passed the Employee object, which needs to be persisted. This is done using the keyword this, which passes the instance of the Employee object on which Save() was called.

# Storing and Loading with Files

The actual implementation of the Store() method inside DataStorage involves classes within the System.IO namespace, as shown in Listing 6.13. Inside Store(), you begin by instantiating a FileStream object that you associate with a file corresponding to the employee's full name. The FileMode.Create parameter indicates that you want a new file to be created if there isn't already one with the <firstname><lastname>.dat name; if the file exists already, it will be overwritten. Next, you create a StreamWriter class. The StreamWriter class is responsible for writing text into the FileStream. You write the data using WriteLine() methods, just as though writing to the console.

```
LISTING 6.13: Data Persistence to a File
using System;
// IO namespace
using System.IO;

class DataStorage
{
 // Save an employee object to a file
 // named with the Employee name.
 // Error handling not shown.
```