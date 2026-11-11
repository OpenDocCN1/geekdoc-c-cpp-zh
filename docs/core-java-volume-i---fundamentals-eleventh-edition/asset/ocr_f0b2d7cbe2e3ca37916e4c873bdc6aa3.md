# ### 3.6.2 Concatenation

Java, like most programming languages, allows you to use + to join (concatenate) two strings.

```
```java
String expletive = "Expletive";
String PG13 = "deleted";
String message = expletive + PG13;
```
```

The preceding code sets the variable *message* to the string "Expletivedeleted". (Note the lack of a space between the words: The + operator joins two strings in the order received, *exactly* as they are given.)

When you concatenate a string with a value that is not a string, the latter is converted to a string. (As you will see in Chapter 5, every Java object can be converted to a string.) For example,

```
```java
int age = 13;
String rating = "PG" + age;
```
```

sets rating to the string "PG13".

This feature is commonly used in output statements. For example,

```
```java
System.out.println("The answer is " + answer);
```
```

is perfectly acceptable and prints what you would expect (and with correct spacing because of the space after the word *is*).

If you need to put multiple strings together, separated by a delimiter, use the static join method:

```
```java
String all = String.join(" / ", "S", "M", "L", "XL");
// all is the string "S / M / L / XL"
```
```

As of Java 11, there is a repeat method:

```
```java
String repeated = "Java".repeat(3); // repeated is "JavaJavaJava"
```
```

# ### 3.6.3 Strings Are Immutable

The String class gives no methods that let you *change* a character in an existing string. If you want to turn *greeting* into "Help!", you cannot directly change the last positions of *greeting* into 'p' and '!'. If you are a C programmer, this can make you feel pretty helpless. How are we going to modify the string? In Java, it is quite easy: Concatenate the substring that you want to keep with the characters that you want to replace.

```
```java
greeting = greeting.substring(0, 3) + "p!";
```
```