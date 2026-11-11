
```java
greeting = "Howdy";
```

Don't we have a memory leak? After all, the original string was allocated on the heap. Fortunately, Java does automatic garbage collection. If a block of memory is no longer needed, it will eventually be recycled.

If you are a C++ programmer and use the `string` class defined by ANSI C++, you will be much more comfortable with the Java `String` type. C++ `string` objects also perform automatic allocation and deallocation of memory. The memory management is performed explicitly by constructors, assignment operators, and destructors. However, C++ strings are mutable—you can modify individual characters in a string.

### 3.6.4 Testing Strings for Equality

To test whether two strings are equal, use the `equals` method. The expression

```java
s.equals(t)
```

returns `true` if the strings `s` and `t` are equal, `false` otherwise. Note that `s` and `t` can be string variables or string literals. For example, the expression

```java
"Hello".equals(greeting)
```

is perfectly legal. To test whether two strings are identical except for the upper/lowercase letter distinction, use the `equalsIgnoreCase` method.

```java
"Hello".equalsIgnoreCase("hello")
```

Do *not* use the `==` operator to test whether two strings are equal! It only determines whether or not the strings are stored in the same location. Sure, if strings are in the same location, they must be equal. But it is entirely possible to store multiple copies of identical strings in different places.

```java
String greeting = "Hello"; // initialize greeting to a string
if (greeting == "Hello") . . .
    // probably true
if (greeting.substring(0, 3) == "Hel") . . .
    // probably false
```

If the virtual machine always arranges for equal strings to be shared, then you could use the `==` operator for testing equality. But only string literals are shared, not strings that are the result of operations like `+` or `substring`. Therefore, never use `==` to compare strings lest you end up with a program with the worst kind of bug—an intermittent one that seems to occur randomly.

> **C++ NOTE:** If you are used to the C++ string class, you have to be particularly careful about equality testing. The C++ string class does overload the == operator to test for equality of the string contents. It is perhaps unfortunate that Java goes out of its way to give strings the same “look and feel” as numeric values but then makes strings behave like pointers for equality testing. The language designers could have redefined == for strings, just as they made a special arrangement for +. Oh well, every language has its share of inconsistencies.
> 
> C programmers never use == to compare strings but use `strcmp` instead. The Java method `compareTo` is the exact analog of `strcmp`. You can use
> 
> `if (greeting.compareTo("Hello") == 0) . . .`
> 
> but it seems clearer to use `equals` instead.

### 3.6.5 Empty and Null Strings

The empty string `""` is a string of length 0. You can test whether a string is empty by calling

```java
if (str.length() == 0)
```

or

```java
if (str.equals(""))
```

An empty string is a Java object which holds the string length (namely, 0) and an empty contents. However, a String variable can also hold a special value, called null, that indicates that no object is currently associated with the variable. (See Chapter 4 for more information about null.) To test whether a string is null, use

```java
if (str == null)
```

Sometimes, you need to test that a string is neither null nor empty. Then use

```java
if (str != null && str.length() != 0)
```

You need to test that str is not null first. As you will see in Chapter 4, it is an error to invoke a method on a null value.

### 3.6.6 Code Points and Code Units

Java strings are sequences of char values. As we discussed in Section 3.3.3, “The char Type,” on p. 46, the char data type is a code unit for representing Unicode code points in the UTF-16 encoding. The most commonly used Unicode characters can be represented with a single code unit. The supplementary characters require a pair of code units.

The length method yields the number of code units required for a given string in the UTF-16 encoding. For example:

```java
String greeting = "Hello";
int n = greeting.length(); // is 5
```

To get the true length—that is, the number of code points—call

```java
int cpCount = greeting.codePointCount(0, greeting.length());
```

The call s.charAt(n) returns the code unit at position n, where n is between 0 and s.length() − 1. For example:

```java
char first = greeting.charAt(0); // first is 'H'
char last = greeting.charAt(4); // last is 'o'
```

To get at the ith code point, use the statements

```java
int index = greeting.offsetByCodePoints(0, i);
int cp = greeting.codePointAt(index);
```

Why are we making a fuss about code units? Consider the sentence

𝕆 is the set of octonions.

The character 𝕆 (U+1D546) requires two code units in the UTF-16 encoding. Calling

```java
char ch = sentence.charAt(1)
```

doesn’t return a space but the second code unit of 𝕆. To avoid this problem, you should not use the char type. It is too low-level.

> **NOTE:** Don’t think that you can ignore exotic characters with code units above U+FFFF. Your emoji-loving users may put characters such as 🍺 (U+1F37A, beer mug) into strings.

If your code traverses a string, and you want to look at each code point in turn, you can use these statements:

```java
int cp = sentence.codePointAt(i);
if (Character.isSupplementaryCodePoint(cp)) i += 2;
else i++;
```

You can move backwards with the following statements:

```java
i--;
if (Character.isSurrogate(sentence.charAt(i))) i--;
int cp = sentence.codePointAt(i);
```

Obviously, that is quite painful. An easier way is to use the `codePoints` method that yields a “stream” of int values, one for each code point. (We will discuss streams in Chapter 2 of Volume II.) You can just turn the stream into an array (see Section 3.10, “Arrays,” on p. 108) and traverse that.

```java
int[] codePoints = str.codePoints().toArray();
```

Conversely, to turn an array of code points to a string, use a *constructor*. (We discuss constructors and the `new` operator in detail in Chapter 4.)

```java
String str = new String(codePoints, 0, codePoints.length);
```

> **NOTE:** The virtual machine does not have to implement strings as sequences of code units. In Java 9, strings that hold only single-byte code units use a byte array, and all others a char array.

### 3.6.7 The String API

The `String` class in Java contains more than 50 methods. A surprisingly large number of them are sufficiently useful that we can imagine using them frequently. The following API note summarizes the ones we found most useful.

These API notes, found throughout the book, will help you understand the Java Application Programming Interface (API). Each API note starts with the name of a class, such as `java.lang.String`. (The significance of the so-called *package* name `java.lang` is explained in Chapter 4.) The class name is followed by the names, explanations, and parameter descriptions of one or more methods.

We typically do not list all methods of a particular class but select those that are most commonly used and describe them in a concise form. For a full listing, consult the online documentation (see Section 3.6.8, “Reading the Online API Documentation,” on p. 71).

We also list the version number in which a particular class was introduced. If a method has been added later, it has a separate version number.

**java.lang.String** 1.0

- `char charAt(int index)`  
  returns the code unit at the specified location. You probably don't want to call this method unless you are interested in low-level code units.

- `int codePointAt(int index)` 5  
  returns the code point that starts at the specified location.

- `int offsetByCodePoints(int startIndex, int cpCount)` 5  
  returns the index of the code point that is `cpCount` code points away from the code point at `startIndex`.

- `int compareTo(String other)`  
  returns a negative value if the string comes before other in dictionary order, a positive value if the string comes after other in dictionary order, or 0 if the strings are equal.

- `IntStream codePoints()` 8  
  returns the code points of this string as a stream. Call `toArray` to put them in an array.

- `new String(int[] codePoints, int offset, int count)` 5  
  constructs a string with the count code points in the array starting at offset.

- `boolean isEmpty()`

- `boolean isBlank()` 11  
  returns true if the string is empty or consists of whitespace.

- `boolean equals(Object other)`  
  returns true if the string equals other.

- `boolean equalsIgnoreCase(String other)`  
  returns true if the string equals other, except for upper/lowercase distinction.

- `boolean startsWith(String prefix)`

- `boolean endsWith(String suffix)`  
  returns true if the string starts with prefix or ends with suffix.

- `int indexOf(String str)`

- `int indexOf(String str, int fromIndex)`

- `int indexOf(int cp)`

- `int indexOf(int cp, int fromIndex)`  
  returns the start of the first substring equal to the string `str` or the code point `cp`, starting at index 0 or at `fromIndex`, or -1 if `str` does not occur in this string.
