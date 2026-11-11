```
```java
String repeated = "Java".repeat(3); // repeated is
"JavaJavaJava"
```
```

# ### 3.6.3 Strings Are Immutable

The String class gives no methods that let you *change* a character in an existing string. If you want to turn greeting into "Help!", you cannot directly change the last positions of greeting into 'p' and '!'. If you are a C programmer, this can make you feel pretty helpless. How are we going to modify the string? In Java, it is quite easy: Concatenate the substring that you want to keep with the characters that you want to replace.

```
```java
String greeting = "Hello";
greeting = greeting.substring(0, 3) + "p!";
```
```

This declaration changes the current value of the greeting variable to "Help!".

Since you cannot change the individual characters in a Java string, the documentation refers to the objects of the String class as *immutable*. Just as the number 3 is always 3, the string "Hello" will always contain the code-unit sequence for the characters h,e,l,l,o. You cannot change these values. Yet you can, as you just saw, change the contents of the string variable greeting and make it refer to a different string, just as you can make a numeric variable currently holding the value 3 hold the value 4.

Isn’t that a lot less efficient? It would seem simpler to change the code units than to build up a whole new string from scratch. Well, yes and no. Indeed, it isn’t efficient to generate a new string that holds the concatenation of "Hel" and "p!". But immutable strings have one great advantage: The compiler can arrange that strings are *shared*.

To understand how this works, think of the various strings as sitting in a common pool. String variables then point to locations in the pool. If you copy a string variable, both the original and the copy share the same characters.