Obviously, that is quite painful. An easier way is to use the `codePoints` method that yields a “stream” of int values, one for each code point. (We will discuss streams in Chapter 2 of Volume II.) You can just turn the stream into an array (see Section 3.10, “Arrays,” on p. 108) and traverse that.

```
int[] codePoints = str.codePoints().toArray();
```

Conversely, to turn an array of code points to a string, use a *constructor*. (We discuss constructors and the `new` operator in detail in Chapter 4.)

```
String str = new String(codePoints, 0, codePoints.length);
```

> > **NOTE:** The virtual machine does not have to implement strings as sequences of code units. In Java 9, strings that hold only single-byte code units use a byte array, and all others a char array.

# ### 3.6.7 The String API

The `String` class in Java contains more than 50 methods. A surprisingly large number of them are sufficiently useful that we can imagine using them frequently. The following API note summarizes the ones we found most useful.

These API notes, found throughout the book, will help you understand the Java Application Programming Interface (API). Each API note starts with the name of a class, such as `java.lang.String`. (The significance of the so-called *package* name `java.lang` is explained in Chapter 4.) The class name is followed by the names, explanations, and parameter descriptions of one or more methods.

We typically do not list all methods of a particular class but select those that are most commonly used and describe them in a concise form. For a full listing, consult the online documentation (see Section 3.6.8, “Reading the Online API Documentation,” on p. 71).

We also list the version number in which a particular class was introduced. If a method has been added later, it has a separate version number.

**java.lang.String** 1.0

- `char charAt(int index)`
  returns the code unit at the specified location. You probably don't want to call this method unless you are interested in low-level code units.

*(Continues)*