```
```java
private void writeObject(ObjectOutputStream out)
    throws IOException
{
    out.defaultWriteObject();
    out.writeDouble(point.getX());
    out.writeDouble(point.getY());
}
```
```

In the readObject method, we reverse the process:

```
```java
private void readObject(ObjectInputStream in)
    throws IOException
{
    in.defaultReadObject();
    double x = in.readDouble();
    double y = in.readDouble();
    point = new Point2D.Double(x, y);
}
```
```

Another example is the java.util.Date class that supplies its own readObject and writeObject methods. These methods write the date as a number of milliseconds from the epoch (January 1, 1970, midnight UTC). The Date class has a complex internal representation that stores both a Calendar object and a millisecond count to optimize lookups. The state of the Calendar is redundant and does not have to be saved.

The readObject and writeObject methods only need to save and load their data fields. They should not concern themselves with superclass data or any other class information.

Instead of letting the serialization mechanism save and restore object data, a class can define its own mechanism. To do this, a class must implement the *Externalizable* interface. This, in turn, requires it to define two methods:

```
```java
public void readExternal(ObjectInputStream in)
    throws IOException, ClassNotFoundException;
public void writeExternal(ObjectOutputStream out)
    throws IOException;
```
```

Unlike the readObject and writeObject methods that were described in the previous section, these methods are fully responsible for saving and restoring the entire object, *including the superclass data*. When writing an object, the serialization mechanism merely records the class of the object in the output stream. When reading an externalizable object, the object input stream creates an object with the no-argument constructor and then calls the readExternal method. Here is how you can implement these methods for the Employee class: