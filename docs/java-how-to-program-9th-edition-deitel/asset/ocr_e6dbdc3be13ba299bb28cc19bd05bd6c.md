```
s1 =
s2 = hello
s3 = birth day
s4 = day
```

Fig. 16.1 | String class constructors. (Part 2 of 2.)

string, which can also be represented as "" and has a length of 0. Line 13 instantiates a new String object using class String’s constructor that takes a String object as an argument and assigns its reference to s2. The new String object contains the same sequence of characters as the String object s that’s passed as an argument to the constructor.

> Software Engineering Observation 16.1
> It’s not necessary to copy an existing String object. String objects are immutable—their character contents cannot be changed after they’re created, because class String does not provide methods that allow the contents of a String object to be modified.

Line 14 instantiates a new String object and assigns its reference to s3 using class String’s constructor that takes a char array as an argument. The new String object contains a copy of the characters in the array.

Line 15 instantiates a new String object and assigns its reference to s4 using class String’s constructor that takes a char array and two integers as arguments. The second argument specifies the starting position (the offset) from which characters in the array are accessed. Remember that the first character is at position 0. The third argument specifies the number of characters (the count) to access in the array. The new String object is formed from the accessed characters. If the offset or the count specified as an argument results in accessing an element outside the bounds of the character array, a StringIndexOutOfBoundsException is thrown.

> Common Programming Error 16.1
> Accessing a character outside the bounds of a String (i.e., an index less than 0 or an index greater than or equal to the String’s length) results in a StringIndexOutOfBoundsException.

# 16.3.2 String Methods length, charAt and getChars

String methods length, charAt and getChars return the length of a String, obtain the character at a specific location in a String and retrieve a set of characters from a String as a char array, respectively. Figure 16.2 demonstrates each of these methods.

```
1  // Fig. 16.2: StringMiscellaneous.java
2  // This application demonstrates the length, charAt and getChars
3  // methods of the String class.
4
5  public class StringMiscellaneous
6  {
```

Fig. 16.2 | String methods length, charAt and getChars. (Part 1 of 2.)