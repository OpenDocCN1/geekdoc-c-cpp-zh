| `java.util.zip.ZipFile` | `1.1` |
|---|---|
| • `ZipFile(String name)`<br>• `ZipFile(File file)`<br>creates a ZipFile for reading from the given string or File object.<br><br>• `Enumeration entries()`<br>returns an Enumeration object that enumerates the ZipEntry objects that describe the entries of the ZipFile.<br><br>• `ZipEntry getEntry(String name)`<br>returns the entry corresponding to the given name, or null if there is no such entry.<br><br>• `InputStream getInputStream(ZipEntry ze)`<br>returns an InputStream for the given entry.<br><br>• `String getName()`<br>returns the path of this ZIP file. |

# 2.3 Object Input/Output Streams and Serialization

Using a fixed-length record format is a good choice if you need to store data of the same type. However, objects that you create in an object-oriented program are rarely all of the same type. For example, you might have an array called staff that is nominally an array of Employee records but contains objects that are actually instances of a subclass such as Manager.

It is certainly possible to come up with a data format that allows you to store such polymorphic collections—but, fortunately, we don’t have to. The Java language supports a very general mechanism, called object serialization, that makes it possible to write any object to an output stream and read it again later. (You will see in this chapter where the term “serialization” comes from.)

# 2.3.1 Saving and Loading Serializable Objects

To save object data, you first need to open an ObjectOutputStream object:

```
var out = new ObjectOutputStream(new FileOutputStream("employee.dat"));
```

Now, to save an object, simply use the writeObject method of the ObjectOutputStream class as in the following fragment:

```
var harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);
var boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
```