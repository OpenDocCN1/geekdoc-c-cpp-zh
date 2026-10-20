# Chapter 16 Strings, Characters and Regular Expressions

```
```java
// test compareTo
System.out.printf(
"\nsl.compareTo( s2 ) is %d", s1.compareTo( s2 ) );
System.out.printf(
"\ns2.compareTo( s1 ) is %d", s2.compareTo( s1 ) );
System.out.printf(
"\nsl.compareTo( s1 ) is %d", s1.compareTo( s1 ) );
System.out.printf(
"\ns3.compareTo( s4 ) is %d", s3.compareTo( s4 ) );
System.out.printf(
"\ns4.compareTo( s3 ) is %d\n\n", s4.compareTo( s3 ) );
```
```

```
```java
if ( s3.regionMatches( 0, s4, 0, 5 ) )
	System.out.println( "First 5 characters of s3 and s4 match" );
else
	System.out.println( "First 5 characters of s3 and s4 do not match" );
```
```

```
```java
if ( s3.regionMatches( true, 0, s4, 0, 5 ) )
	System.out.println( "First 5 characters of s3 and s4 match with case ignored" );
else
	System.out.println( "First 5 characters of s3 and s4 do not match" );
```
```

```
s1 = hello
s2 = goodbye
s3 = Happy Birthday
s4 = happy birthday
s1 equals "hello"
s1 is not the same object as "hello"
Happy Birthday equals happy birthday with case ignored
s1.compareTo( s2 ) is 1
s2.compareTo( s1 ) is -1
s1.compareTo( s1 ) is 0
s3.compareTo( s4 ) is -32
s4.compareTo( s3 ) is 32
First 5 characters of s3 and s4 do not match
First 5 characters of s3 and s4 match with case ignored
```

Fig. 16.3 | String methods equals, equalsIgnoreCase, compareTo and regionMatches. (Part 2 of 2.)

# String Method equals

The condition at line 17 uses method equals to compare String s1 and the String literal "hello" for equality. Method equals (a method of class Object overridden in String) tests any two objects for equality—the strings contained in the two objects are identical.