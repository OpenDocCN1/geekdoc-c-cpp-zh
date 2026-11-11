```
out.writeObject(harry);
out.writeObject(boss);
```

To read the objects back in, first get an ObjectInputStream object:

```
var in = new ObjectInputStream(new FileInputStream("employee.dat"));
```

Then, retrieve the objects in the same order in which they were written, using the readObject method:

```
var e1 = (Employee) in.readObject();
var e2 = (Employee) in.readObject();
```

There is, however, one change you need to make to any class that you want to save to an output stream and restore from an object input stream. The class must implement the Serializable interface:

```
class Employee implements Serializable { . . . }
```

The Serializable interface has no methods, so you don’t need to change your classes in any way. In this regard, it is similar to the Cloneable interface that we discussed in Volume I, Chapter 6. However, to make a class cloneable, you still had to override the clone method of the Object class. To make a class serializable, you do not need to do anything else.

> **NOTE:** You can write and read only *objects* with the `writeObject`/`readObject` methods. For primitive type values, use methods such as `writeInt`/`readInt` or `writeDouble`/`readDouble`. (The object input/output stream classes implement the `DataInput`/`DataOutput` interfaces.)

Behind the scenes, an ObjectOutputStream looks at all the fields of the objects and saves their contents. For example, when writing an Employee object, the name, date, and salary fields are written to the output stream.

However, there is one important situation to consider: What happens when one object is shared by several objects as part of their state?

To illustrate the problem, let us make a slight modification to the Manager class. Let’s assume that each manager has a secretary:

```
class Manager extends Employee
{
    private Employee secretary;
    . . .
}
```