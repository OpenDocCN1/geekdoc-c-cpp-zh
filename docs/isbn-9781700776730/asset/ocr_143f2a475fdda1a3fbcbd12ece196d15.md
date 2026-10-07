Second, because there is such a close relationship between a string literal (which is type char*) and the String class, it should be easy to create a String object based upon that literal. In this case a separate copy of the literal must be made so that it can be encapsulated as part of the class.

```
String(const char*);
```

Third, it might be useful to be able to create a String object from a single character.

```
String(char);
```

Fourth, here is a constructor that creates a String object from an int value. This implies allocating int bytes from the heap, and setting the first byte to the NULL character. Note that a value less than zero should be interpreted as zero.

```
String(int);
```

Recall from our discussion on copy constructors that the compiler automatically supplies one for you if you fail to write one. This is fine if a class contains no pointer members, but will cause a big problem if at least one pointer data member is present. The reason for this is that two or more pointer members may not point to the same space on the heap, and this is exactly what would happen if you used the default copy constructor. Therefore, it is now necessary to create one for the String class.

```
String(const String&);
```