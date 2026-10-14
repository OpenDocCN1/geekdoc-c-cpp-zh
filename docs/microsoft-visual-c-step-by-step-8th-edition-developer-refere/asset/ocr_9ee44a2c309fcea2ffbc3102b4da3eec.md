```
ScreenPosition location;
location.X = 40; // compile-time error, location not assigned
```

# Note

This might seem trivial, but if X were a field rather than a property, the code would be legal. For this reason, you should define structures and classes from the beginning by using properties rather than fields that you later migrate to properties. Code that uses your classes and structures might no longer work after you change fields into properties. You will return to this matter in the section “Generating automatic properties” later in this chapter.

+   You can’t use a property as a ref or an out argument to a method (although you can use a writable field as a ref or an out argument). This makes sense because the property doesn’t really point to a memory location; rather, it points to an accessor method, such as in the following example:

Click here to view code image

```
MyMethod(ref location.X); // compile-time error
```

+   A property can contain at most one get accessor and one set accessor. A property cannot contain other methods, fields, or properties.

+   The get and set accessors cannot take any parameters. The data being assigned is passed to the set accessor automatically by using the value variable.

+   You can’t declare properties by using const, such as is demonstrated here:

Click here to view code image

```
const int X { get { ... } set { ... } } // compile-time error
```