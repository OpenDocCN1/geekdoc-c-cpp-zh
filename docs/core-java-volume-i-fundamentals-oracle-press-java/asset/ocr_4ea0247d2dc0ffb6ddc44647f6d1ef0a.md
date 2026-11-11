Don’t we have a memory leak? After all, the original string was allocated on the heap. Fortunately, Java does automatic garbage collection. If a block of memory is no longer needed, it will eventually be recycled.

If you are a C++ programmer and use the string class defined by ANSI C++, you will be much more comfortable with the Java string type. C++ string objects also perform automatic allocation and deallocation of memory. The memory management is performed explicitly by constructors, assignment operators, and destructors. However, C++ strings are mutable—you can modify individual characters in a string.

# 3.6.4 Testing Strings for Equality

To test whether two strings are equal, use the `equals` method. The expression

```
```java
s.equals(t)
```
```

returns true if the strings s and t are equal, false otherwise. Note that s and t can be string variables or string literals.

For example, the expression

```
```java
"Hello".equals(greeting)
```
```

is perfectly legal. To test whether two strings are identical except for the upper/lowercase letter distinction, use the `equalsIgnoreCase` method.

```
```java
"Hello".equalsIgnoreCase("hello")
```
```

Do *not* use the `==` operator to test whether two strings are equal! It only determines whether or not the strings are stored in the same location. Sure, if strings are in the same location, they must be equal. But it is entirely possible to store multiple copies of identical strings in different places.