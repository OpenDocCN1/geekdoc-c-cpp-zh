
String letters from which characters are to be copied. The substring returned contains a copy of the characters from the starting index to the end of the String. Specifying an index outside the bounds of the String causes a StringIndexOutOfBoundsException.

Line 15 uses the substring method that takes two integer arguments—the starting index from which to copy characters in the original String and the index one beyond the last character to copy (i.e., copy up to, but not including, that index in the String). The substring returned contains a copy of the specified characters from the original String. An index outside the bounds of the String causes a StringIndexOutOfBoundsException.

## 16.3.6 Concatenating Strings

String method concat (Fig. 16.7) concatenates two String objects and returns a new String object containing the characters from both original Strings. The expression s1.concat( s2 ) at line 13 forms a String by appending the characters in s2 to the characters in s1. The original Strings to which s1 and s2 refer are not modified.

```
1  // Fig. 16.7: StringConcatenation.java
2  // String method concat.
3
4  public class StringConcatenation
5  {
6      public static void main( String[] args )
7      {
8          String s1 = "Happy ";
9          String s2 = "Birthday";
10
11         System.out.printf( "s1 = %s\ns2 = %s\n\n",s1, s2 );
12         System.out.printf(
13         "Result of s1.concat( s2 ) = %s\n", s1.concat( s2 ) );
14         System.out.printf( "s1 after concatenation = %s\n", s1 );
15     } // end main
16  } // end class StringConcatenation
```

s1 = Happy
s2 = Birthday

Result of s1.concat( s2 ) = Happy Birthday
s1 after concatenation = Happy

Fig. 16.7 | String method concat.

## 16.3.7 Miscellaneous String Methods

Class String provides several methods that return modified copies of Strings or that return character arrays. These methods are demonstrated in the application in Fig. 16.8.

Line 16 uses String method replace to return a new String object in which every occurrence in s1 of character 'l' (lowercase el) is replaced with character 'L'. Method replace leaves the original String unchanged. If there are no occurrences of the first argument in the String, method replace returns the original String. An overloaded version of method replace enables you to replace substrings rather than individual characters.

// Fig. 16.8: StringMiscellaneous2.java
// String methods replace, toLowerCase, toUpperCase, trim and toCharArray.

public class StringMiscellaneous2
{
    public static void main( String[] args )
    {
        String s1 = "hello";
        String s2 = "GOODBYE";
        String s3 = "   spaces   ";

        System.out.printf( "s1 = %s\ns2 = %s\ns3 = %s\n\n", s1, s2, s3 );

        // test method replace
        System.out.printf(
            "Replace 'l' with 'L' in s1: %s\n\n", s1.replace( 'l', 'L' ) );

        // test toLowerCase and toUpperCase
        System.out.printf( "s1.toUpperCase() = %s\n", s1.toUpperCase() );
        System.out.printf( "s2.toLowerCase() = %s\n\n", s2.toLowerCase() );

        // test trim method
        System.out.printf( "s3 after trim = \"%s\"\n\n", s3.trim() );

        // test toCharArray method
        char[] charArray = s1.toCharArray();
        System.out.print( "s1 as a character array = " );

        for ( char character : charArray )
            System.out.print( character );

        System.out.println();
    } // end main
} // end class StringMiscellaneous2

```
s1 = hello
s2 = GOODBYE
s3 =    spaces   

Replace 'l' with 'L' in s1: heLLo

s1.toUpperCase() = HELLO
s2.toLowerCase() = goodbye

s3 after trim = "spaces"

s1 as a character array = hello
```

Fig. 16.8 | String methods replace, toLowerCase, toUpperCase, trim and toCharArray.

Line 19 uses String method toUpperCase to generate a new String with uppercase letters where corresponding lowercase letters exist in s1. The method returns a new String object containing the converted String and leaves the original String unchanged. If there are no characters to convert, method toUpperCase returns the original String.

Line 20 uses String method toLowerCase to return a new String object with lowercase letters where corresponding uppercase letters exist in s2. The original String remains unchanged. If there are no characters in the original String to convert, toLowerCase returns the original String.

Line 23 uses String method trim to generate a new String object that removes all white-space characters that appear at the beginning and/or end of the String on which trim operates. The method returns a new String object containing the String without leading or trailing white space. The original String remains unchanged. If there are no whitespace characters at the beginning and/or end, trim returns the original String.

Line 26 uses String method toCharArray to create a new character array containing a copy of the characters in s1. Lines 29–30 output each char in the array.

## 16.3.8 String Method valueOf

As we’ve seen, every object in Java has a toString method that enables a program to obtain the object’s string representation. Unfortunately, this technique cannot be used with primitive types because they do not have methods. Class String provides static methods that take an argument of any type and convert it to a String object. Figure 16.9 demonstrates the String class valueOf methods.

The expression String.valueOf(charArray) at line 18 uses the character array charArray to create a new String object. The expression String.valueOf(charArray, 3, 3) at line 20 uses a portion of the character array charArray to create a new String object. The second argument specifies the starting index from which the characters are used. The third argument specifies the number of characters to be used.

```
1  // Fig. 16.9: StringValueOf.java
2  // String valueOf methods.
3
4  public class StringValueOf
5  {
6      public static void main( String[] args )
7      {
8          char[] charArray = { 'a', 'b', 'c', 'd', 'e', 'f' };
9          boolean booleanValue = true;
10         char characterValue = 'Z';
11         int integerValue = 7;
12         long longValue = 10000000000L; // L suffix indicates long
13         float floatValue = 2.5f; // f indicates that 2.5 is a float
14         double doubleValue = 33.333; // no suffix, double is default
15         Object objectRef = "hello"; // assign string to an Object reference
16
17         System.out.printf(
18             "char array = %s\n", String.valueOf( charArray ) );
19         System.out.printf( "part of char array = %s\n",
20             String.valueOf( charArray, 3, 3 ) );
21         System.out.printf(
22             "boolean = %s\n", String.valueOf( booleanValue ) );
23         System.out.printf(
24             "char = %s\n", String.valueOf( characterValue ) );
```

```
25        System.out.printf( "int = %s\n", String.valueOf( integerValue ) );
26        System.out.printf( "long = %s\n", String.valueOf( longValue ) );
27        System.out.printf( "float = %s\n", String.valueOf( floatValue ) );
28        System.out.printf(
29            "double = %s\n", String.valueOf( doubleValue ) );
30        System.out.printf( "Object = %s", String.valueOf( objectRef ) );
31    } // end main
32 } // end class StringValueOf
```

```
char array = abcdef
part of char array = def
boolean = true
char = Z
int = 7
long = 10000000000
float = 2.5
double = 33.333
Object = hello
```

Fig. 16.9 | String valueOf methods. (Part 2 of 2.)

There are seven other versions of method valueOf, which take arguments of type boolean, char, int, long, float, double and Object, respectively. These are demonstrated in lines 21–30. The version of valueOf that takes an Object as an argument can do so because all Objects can be converted to Strings with method toString.

> [Note: Lines 12–13 use literal values 10000000000L and 2.5f as the initial values of long variable longValue and float variable floatValue, respectively. By default, Java treats integer literals as type int and floating-point literals as type double. Appending the letter L to the literal 10000000000 and appending letter f to the literal 2.5 indicates to the compiler that 10000000000 should be treated as a long and 2.5 as a float. An uppercase L or lowercase l can be used to denote a variable of type long and an uppercase F or lowercase f can be used to denote a variable of type float.]

## 16.4 Class StringBuilder

We now discuss the features of class StringBuilder for creating and manipulating dynamic string information—that is, modifiable strings. Every StringBuilder is capable of storing a number of characters specified by its capacity. If a StringBuilder’s capacity is exceeded, the capacity expands to accommodate the additional characters.

Performance Tip 16.2
Java can perform certain optimizations involving String objects (such as referring to one String object from multiple variables) because it knows these objects will not change. Strings (not StringBuilders) should be used if the data will not change.

Performance Tip 16.3
In programs that frequently perform string concatenation, or other string modifications, it’s often more efficient to implement the modifications with class StringBuilder.
