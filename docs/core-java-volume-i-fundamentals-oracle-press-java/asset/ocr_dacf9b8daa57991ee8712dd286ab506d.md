```
```java
String greeting = "Hello";
int n = greeting.length(); // is 5
```
```

To get the true length—that is, the number of code points—call

```
```java
int cpCount = greeting.codePointCount(0, greeting.length());
```
```

The `s.charAt(n)` returns the code unit at position n, where n is between 0 and `s.length() − 1`. For example:

```
```java
char first = greeting.charAt(0); // first is 'H'
char last = greeting.charAt(4);  // last is 'o'
```
```

To get at the ith code point, use the statements

```
```java
int index = greeting.offsetByCodePoints(0, i);
int cp = greeting.codePointAt(index);
```
```

What is the fuss about code units? Consider the sentence

𝕆 is the set of octonions.

The character (U+1D546) requires two code units in the UTF-16 encoding. Calling

```
```java
char ch = sentence.charAt(1)
```
```

doesn’t return a space but the second code unit of 𝕆. To avoid this problem, you should not use the char type. It is too low-level.

> **NOTE:**