actual type (Form), which supports the Text property. The CType command (covered later) accepts the object as its first parameter, and the class name (without quotes) as its second parameter. In this case, the current instance variable is of type Form; and by casting this variable, the code can reference the Text property of the current form.

# The String Class

Another class that plays a large role in most development projects is the String class. The String class is a special class within .NET because it is the one primitive type that is not a value type. To make String objects compatible with some of the underlying behavior in .NET, they have some interesting characteristics.

These methods are shared, which means that the methods are not specific to any instance of a String. The String class also contains several other methods that are called based on an instance of a specific String object. The methods on the String class replace the functions that Visual Basic 6.0 had as part of the language for string manipulation, and they perform operations such as inserting strings, splitting strings, and searching strings.

# String()

The String class has several different constructors for those situations in which you aren’t simply assigning an existing value to a new string. The term constructor is expanded upon in Chapter 3. Constructors are methods that are used to construct an instance of a class. String() would be the default constructor for the String class, but the String class does not expose this constructor publicly. The following example shows some of the most common methods for creating a String. This example method does not show the end of this Sub because it will be used for all of the string-related examples, with the output from these methods shown together. The following code snippet is the start of a method; the End Sub is not shown. The full Sub in the code download is the concatenation of this snippet with the next five snippets. You can build and test these parts sequentially.

```
Private Sub StringSamples()
    Dim strSample As String = "ABC"
    Dim strSample2 = "DEF"
    Dim strSample3 = New String("A"c, 20)
    Dim line = New String("-", 80)
```

Code snippet from Form1

A variable is declared of type String and as a primitive is assigned the value "ABC." The second declaration uses one of the parameterized versions of the String constructor. This constructor accepts two parameters: The first is a character and the second specifies how many times that character should be repeated in the string.

In addition to creating an instance of a string and then calling methods on your variable, the String class has several shared methods. A shared method refers to a method on a class that does not require an instance of that class. Shared methods are covered in more detail in relation to objects in Chapter 3; for the purpose of this chapter, the point is that you can reference the class String followed by a "." and see a list of shared methods for that class. For strings, this list includes the methods described in Table 2-4.

# TABLE 2-4: Methods Available on the Class String

| SHARED METHOD | DESCRIPTION |
|---|---|
| Empty | This is actually a property. It can be used when an empty String is required. It can be used for comparison or initialization of a String. |
| Compare | Compares two objects of type String |
| CompareOrdinal | Compares two Strings, without considering the local national language or culture |