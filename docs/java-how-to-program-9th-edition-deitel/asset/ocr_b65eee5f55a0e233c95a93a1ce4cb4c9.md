```
```java
// test method endsWith
for ( String string : strings )
{
    if ( string.endsWith( "ed" ) )
        System.out.printf( "\"%s\" ends with \"ed\"\n", string );
} // end for
} // end main
} // end class StringStartEnd
```
```

```
"started" starts with "st"
"starting" starts with "st"

"started" starts with "art" at position 2
"starting" starts with "art" at position 2

"started" ends with "ed"
"ended" ends with "ed"
```

Lines 11–15 use the version of method `startsWith` that takes a String argument. The condition in the if statement (line 13) determines whether each String in the array starts with the characters "st". If so, the method returns true and the application prints that String. Otherwise, the method returns false and nothing happens.

Lines 20–25 use the startsWith method that takes a String and an integer as arguments. The integer specifies the index at which the comparison should begin in the String. The condition in the if statement (line 22) determines whether each String in the array has the characters "art" beginning with the third character in each String. If so, the method returns true and the application prints the String.

The third for statement (lines 30–34) uses method endsWith, which takes a String argument. The condition at line 32 determines whether each String in the array ends with the characters "ed". If so, the method returns true and the application prints the String.

# 16.3.4 Locating Characters and Substrings in Strings

Often it’s useful to search a string for a character or set of characters. For example, if you’re creating your own word processor, you might want to provide a capability for searching through documents. Figure 16.5 demonstrates the many versions of String methods **indexOf** and **lastIndexOf** that search for a specified character or substring in a String.

```
```java
// Fig. 16.5: StringIndexMethods.java
// String searching methods indexOf and lastIndexOf.

public class StringIndexMethods
{
    public static void main( String[] args )
    {
        String letters = "abcdefghijklmnopqrstuvwxyz";
```
```