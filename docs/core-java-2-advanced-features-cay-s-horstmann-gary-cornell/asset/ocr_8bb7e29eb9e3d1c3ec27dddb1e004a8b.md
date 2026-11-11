standalone `serialver` program that is part of the JDK to obtain this number. For example, running

```
serialver Employee
```

prints

```
Employee: static final long serialVersionUID = -1814239825517340645L;
```

If you start the `serialver` program with the `-show` option, the program brings up a graphical dialog box (see Figure 2.7).

![](bbox=[0.251, 0.302, 0.826, 0.381])

**Figure 2.7** The graphical version of the `serialver` program

All *later* versions of the class must define the `serialVersionUID` constant to the same fingerprint as the original.

```
~~~java
class Employee implements Serializable // version 1.1
{
    public static final long serialVersionUID = -1814239825517340645L;
}
~~~
```

When a class has a static data member named `serialVersionUID`, it will not compute the fingerprint manually but will use that value instead.

Once that static data member has been placed inside a class, the serialization system is now willing to read in different versions of objects of that class.

If only the methods of the class change, there is no problem with reading the new object data. However, if the data fields change, you may have problems. For example, the old file object may have more or fewer data fields than the one in the program, or the types of the data fields may be different. In that case, the object input stream makes an effort to convert the serialized object to the current version of the class.

The object input stream compares the data fields of the current version of the class with those of the version in the serialized object. Of course, the object input stream considers only the nontransient and nonstatic data fields. If two fields have matching names but different types, the object input stream makes no effort to convert one type to the other—the objects are incompatible. If the serialized