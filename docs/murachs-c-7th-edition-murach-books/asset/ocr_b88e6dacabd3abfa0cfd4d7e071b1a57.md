# The Type class

| Property | Description |
|---|---|
| Name | Returns a string that contains the name of a type. |
| FullName | Returns a string that contains the fully qualified name of a type, which includes the namespace name and the type name. |
| BaseType | Returns a Type object that represents the class that a type inherits. |
| Namespace | Returns a string that contains the name of the namespace that contains a type. |
| Method | Description |
| GetType() | Returns a Type object that represents the type of an object. |

# Code that uses the Type class to get information about an object

```
Product p;
p = new Book("C#", "Murach's C#", "Anne Boehm", 59.50m);
Type t = p.GetType();
Console.WriteLine("Name: " + t.Name);
Console.WriteLine("Namespace: " + t.Namespace);
Console.WriteLine("FullName: " + t.FullName);
Console.WriteLine("BaseType: " + t.BaseType.Name);
```

# The result that's displayed on the console

Name: Book
Namespace: ProductMaintenance
FullName: ProductMaintenance.Book
BaseType: Product

# How to test an object's type

```
if (p.GetType() == typeof(Book))
```

# Another way to test an object's type

```
if (p.GetType().Name == nameof(Book))
```

# Description

+   - Every object has a GetType() method that returns a Type object that corresponds to the object's type.
+   - You can use the properties of the Type class to obtain information about the type of any object, such as the type's name and the name of its base class.
+   - The properties and methods shown above are only some of the more than 90 properties and methods of the Type class.
+   - The easiest way to test an object's type is to compare the Type object that's returned by the GetType() method of the object with the Type object that's returned by the typeof operator of a type.
+   - Another way to test an object's type is to compare the name of an object's type with the name that's returned by the nameof operator of a type. The nameof operator became available with C# 6.0.