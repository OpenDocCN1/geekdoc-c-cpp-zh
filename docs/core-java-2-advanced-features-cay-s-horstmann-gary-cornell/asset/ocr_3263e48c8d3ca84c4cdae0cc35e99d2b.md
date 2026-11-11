```
```text
68 6A 81 01 48 59 74 19 03    Fingerprint and flags
00 00                         No instance variables
78                            End marker
70                            No superclass
77 08                         External storage, number of bytes
00 00 00 83 E9 39 E0 00       Date
78                            End marker
74 00 0C Carl Cracker          name field value: String (serial #10)
73                            secretay field value: new object (serial #11)
71 00 7E 00 04                existing class (use serial #4)
40 E8 6A 00 00 00 00 00       salary field value: double
73                            hireDay field value: new object (serial #12)
71 00 7E 00 08                Existing class (use serial #8)
77 08                         External storage, number of bytes
00 00 00 91 1B 4E 01 80       Date
78                            End marker
74 00 0C Harry Hacker         name field value: String (serial #13)
71 00 7E 00 08                staff[1]: existing object (use serial #11)
73                            staff[2]: new object (serial #14)
71 00 7E 00 02                Existing class (use serial #2)
40 E3 88 00 00 00 00 00       salary field value: double
73                            hireDay field value: new object (serial #15)
71 00 7E 00 08                Existing class (use serial #8)
77 08                         External storage, number of bytes
00 00 00 94 60 3E EC 00 00    Date
78                            End marker
74 00 08 Tony Tester          name field value: String (serial #16)
71 00 7E 00 08                secretay field value: existing object (use serial #11)
```
```

Of course, studying these codes can be about as exciting as reading a phone book. It is not important to know the exact file format (unless you are trying to create an evil effect by modifying the data), but it is still instructive to know that the serialized format has a detailed description of all the objects that it contains, with sufficient detail to allow reconstruction of both objects and arrays of objects.

What you should remember is this:

+   * The serialized format contains the types and data fields of all objects.