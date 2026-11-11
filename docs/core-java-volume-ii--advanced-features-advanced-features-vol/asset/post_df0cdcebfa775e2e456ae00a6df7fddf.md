
```java
public static void main(String[] args) throws ReflectiveOperationException
{
    var belgium = new Country("Belgium", 30510);
    var analyzer = new ObjectAnalyzer();
    System.out.println(analyzer.toString(belgium));
}
```

Now compile both modules and the Demo program:

```bash
javac com.horstmann.util/module-info.java \
    com.horstmann.util/com/horstmann/util/ObjectAnalyzer.java
javac -p com.horstmann.openpkg/module-info.java \
    v2ch09.openpkg/com/horstmann/places/*.java
java -p v2ch09.openpkg:com.horstmann.util -m v2ch09.openpkg/com.horstmann.places.Demo
```

The program will fail with an exception:

```text
Exception in thread "main" java.lang.reflect.InaccessibleObjectException:
    Unable to make field private java.lang.String com.horstmann.places.Country.name
accessible: module v2ch09.openpkg does not "opens com.horstmann.places" to module
com.horstmann.util
```

Of course, in pristine theory, it is wrong to violate encapsulation and poke around in the private members of an object. But mechanisms such as object-relational mapping or XML/JSON binding are so common that the module system must accommodate them.

Using the opens keyword, a module can *open* a package, which enables reflective access to all instances of classes in the given package. Here is what our module has to do:

```java
module v2ch09.openpkg
{
    requires com.horstmann.util;
    opens com.horstmann.places;
}
```

With this change, the ObjectAnalyzer will work correctly.

A module can be declared as open, such as

```java
open module v2ch09.openpkg
{
    requires com.horstmann.util;
}
```

An open module grants runtime access to all of its packages, as if all packages had been declared with exports and opens. However, only explicitly exported packages are accessible at compile time. Open modules combine the compile-time safety of the module system with the classic permissive runtime behavior.

Recall from Chapter 5 of Volume I that JAR files can contain, in addition to class files and a manifest, *file resources* which can be loaded with the method `Class.getResourceAsStream`, and now also with `Module.getResourceAsStream`. If a resource is stored in a directory that matches a package in a module, then the package must be opened to the caller. Resources in other directories, as well as the class files and manifest, can be read by anyone.

**NOTE:** For a more realistic example, we could convert the `Country` object to XML or JSON. Java 9 and 10 included the `java.xml.bind` module for conversion to XML. That module has been removed from Java 11 (together with the modules `java.activation`, `java.corba`, `java.transaction`, `java.xml.ws`, and `java.xml.ws.annotation`). These modules contain packages that are also part of the Jakarta EE (formerly Java EE) specification, where the APIs are more encompassing than with Java SE. Enterprise application servers cannot be modularized if the JDK has conflicting packages. Unfortunately, as this book is being written, there is no modularized replacement for XML binding.

However, the JSON-B implementation provides modular JAR files if one builds it from source. Hopefully, these JAR files will make it to Maven Central by the time you read this. Place the JAR files on the module path and run the `com.horstmann.places.Demo2` program. When the `com.horstmann.places` package is opened, conversion to JSON succeeds.

**NOTE:** It is possible that future libraries will use *variable handles* instead of reflection for reading and writing fields. A `VarHandle` is similar to a `Field`. You can use it to read or write a specific field of any instance of a specific class. However, to obtain a `VarHandle`, the library code needs a `Lookup` object:

```java
public Object getFieldValue(Object obj, String fieldName, Lookup lookup)
        throws NoSuchFieldException, IllegalAccessException
{
    Class<?> cl = obj.getClass();
    Field field = cl.getDeclaredField(fieldName);
    VarHandle handle = MethodHandles.privateLookupIn(cl, lookup)
            .unreflectVarHandle(field);
    return handle.get(obj);
}
```

This works provided the `Lookup` object is generated in the module that has the permission to access the field. Some method in the module simply calls `MethodHandles.lookup()`, which yields an object encapsulating the access rights of the caller. In this way, one module can give permission for accessing private members to another module. The practical issue is how those permissions can be given with a minimum of hassle.

### 9.8 Automatic Modules

You now know how to put the Java Platform Module System to use. If you start with a brand-new project in which you write all the code yourself, you can design modules, declare module dependencies, and package your application into modular JAR files.

However, that is an extremely uncommon scenario. Almost all projects rely on third-party libraries. Of course, you can wait until the providers of all libraries have turned them into modules, and then modularize your own code.

But what if you don’t want to wait? The Java Platform Module System provides two mechanisms for crossing the chasm that separates today’s premodular world and fully modular applications: *automatic modules* and the *unnamed module*.

For migration purposes, you can turn any JAR file into a module simply by placing it onto a directory in the module path instead of the class path. A JAR without a `module-info.class` on the module path is called an *automatic module*. An automatic module has the following properties:

- 1. The module implicitly has a `requires` clause for all other modules.
- 2. All of its packages are exported and opened.
- 3. If there is an entry with key `Automatic-Module-Name` in the JAR file manifest `META-INF/MANIFEST.MF`, its value becomes the module name.
- 4. Otherwise the module name is obtained from the JAR file name, dropping any trailing version number and replacing sequences of non-alphanumeric characters with a dot.

The first two rules imply that the packages in the automatic module act as if they were on the class path. The reason for using the module path is for the benefit of other modules, allowing them to express dependencies on this module.

Suppose, for example, that you are implementing a module that processes CSV files and uses the Apache Commons CSV library. You would like to express in your `module-info.java` file that your module depends on Apache Commons CSV.

If you add `commons-csv-1.5.jar` onto the module path, then your modules can reference the module. Its name is `commons.csv` since the trailing version number `-1.5` is removed and the non-alphanumeric character `-` is replaced by a dot.

This name might be an acceptable module name because Commons CSV is well known and it is unlikely that someone else will try to use the same name for a different module. But it would be better if the maintainers of this JAR file could quickly agree to reserve a reverse DNS name, preferably the top-level package name `org.apache.commons.csv`, as the module name. They just need to add a line `Automatic-Module-Name: org.apache.commons.csv` to the `META-INF/MANIFEST.MF` file inside the JAR. Eventually, hopefully, they will turn the JAR file into a true module by adding `module-info.java` with the reserved module name—and every other module that refers to the CSV module with that name will just continue to work.

**NOTE:** The migration plan to modules is a great social experiment, and nobody knows whether it will end well. Before you put third-party JARs on the module path, check whether they are modular, and if not, whether their manifest has a module name. If not, you can still turn the JAR into an automatic module, but be prepared to update the module name later.

As this book is being written, version 1.5 of the Commons CSV JAR file does not have a module descriptor or an automatic module name. Nevertheless, it will work fine on the module path. You can download the library from https://commons.apache.org/proper/commons-csv. Uncompress and place the `commons-csv-1.5.jar` file into the directory of the `v2ch09.automod` module. That module contains a simple program that reads a CSV file with country data:

```java
package com.horstmann.places;

import java.io.*;
import org.apache.commons.csv.*;

public class CSVDemo
{
   public static void main(String[] args) throws IOException
   {
      var in = new FileReader("countries.csv");
      Iterable<CSVRecord> records = CSVFormat.EXCEL.withDelimiter(';')
            .withHeader().parse(in);
      for (CSVRecord record : records)
      {
         String name = record.get("Name");
         double area = Double.parseDouble(record.get("Area"));
         System.out.println(name + " has area " + area);
      }
   }
}
```
