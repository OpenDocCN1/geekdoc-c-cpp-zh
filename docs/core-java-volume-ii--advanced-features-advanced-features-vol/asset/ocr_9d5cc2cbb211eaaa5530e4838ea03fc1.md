data fields in all constructors to non-null values, so that the methods don’t have to be prepared to handle null data. It is up to the class designer to implement additional code in the readObject method to fix version incompatibilities or to make sure the methods are robust enough to handle null data.

> **TIP:** Before you add a `serialVersionUID` field to a class, ask yourself why you made your class serializable. If serialization is used only for short-term persistence, such as distributed method calls in an application server, there is no need to worry about versioning and the `serialVersionUID`. The same applies if you extend a class that happens to be serializable, but you have no intent to ever persist its instances. If your IDE gives you pesky warnings, change the IDE preferences to turn them off, or add an annotation (`@SuppressWarnings("serial")`). This is safer than adding a `serialVersionUID` that you may later forget to change.

# 2.3.6 Using Serialization for Cloning

There is an amusing use for the serialization mechanism: It gives you an easy way to clone an object, provided the class is serializable. Simply serialize it to an output stream and then read it back in. The result is a new object that is a deep copy of the existing object. You don’t have to write the object to a file—you can use a `ByteArrayOutputStream` to save the data into a byte array.

As Listing 2.4 shows, to get clone for free, simply extend the `Serializable` class, and you are done.

You should be aware that this method, although clever, will usually be much slower than a clone method that explicitly constructs a new object and copies or clones the data fields.

```
```java
// Listing 2.4  serialClone/SerialCloneTest.java
package serialClone;

/**
 * @version 1.22 2018-05-01
 * @author Cay Horstmann
 */

import java.io.*;
import java.time.*;

public class SerialCloneTest
{
   public static void main(String[] args) throws CloneNotSupportedException
   {
```
```