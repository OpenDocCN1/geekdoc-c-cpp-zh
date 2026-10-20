A string is an object of class String. String literals (stored in memory as String objects) are written as a sequence of characters in double quotation marks, as in:

| "John Q. Doe" | (a name) |
| "9999 Main Street" | (a street address) |
| "Waltham, Massachusetts" | (a city and state) |
| "(201) 555-1212" | (a telephone number) |

A string may be assigned to a String reference. The declaration

```
String color = "blue";
```

initializes String variable color to refer to a String object that contains the string "blue".

# Performance Tip 16.1

> To conserve memory, Java treats all string literals with the same contents as a single String object that has many references to it.

# 16.3 Class String

Class String is used to represent strings in Java. The next several subsections cover many of class String’s capabilities.

# 16.3.1 String Constructors

Class String provides constructors for initializing String objects in a variety of ways. Four of the constructors are demonstrated in the main method of Fig. 16.1.

Line 12 instantiates a new String using class String’s no-argument constructor and assigns its reference to s1. The new String object contains no characters (i.e., the empty

```
1 // Fig. 16.1: StringConstructors.java
2 // String class constructors.
3
4 public class StringConstructors
5 {
6 public static void main( String[] args )
7 {
8 char[] charArray = { 'b', 'i', 'r', 't', 'h', ' ', 'd', 'a', 'y' };
9 String s = new String( "hello" );
10
11 // use String constructors
12 String s1 = new String();
13 String s2 = new String( s );
14 String s3 = new String( charArray );
15 String s4 = new String( charArray, 6, 3 );
16
17 System.out.printf(
18 "s1 = %s\ns2 = %s\ns3 = %s\ns4 = %s\n",
19 s1, s2, s3, s4 ); // display strings
20 } // end main
21 } // end class StringConstructors
```