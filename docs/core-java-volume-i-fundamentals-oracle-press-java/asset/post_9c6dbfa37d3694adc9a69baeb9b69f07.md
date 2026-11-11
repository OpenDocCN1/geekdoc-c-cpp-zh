
There are also >> and << operators which shift a bit pattern right or left. These operators are convenient when you need to build up bit patterns to do bit masking:

```java
int fourthBitFromRight = (n & (1 << 3)) >> 3;
```

Finally, a >>> operator fills the top bits with zero, unlike >> which extends the sign bit into the top bits. There is no <<< operator.

> **CAUTION:**
>
> The right-hand argument of the shift operators is reduced modulo 32 (unless the left-hand argument is a `long`, in which case the right-hand argument is reduced modulo 64). For example, the value of `1 << 35` is the same as `1 << 3` or `8`.

> **C++ NOTE:**
>
> In C/C++, there is no guarantee as to whether >> performs an arithmetic shift (extending the sign bit) or a logical shift (filling in with zeroes). Implementers are free to choose whichever is more efficient. That means the C/C++ >> operator may yield implementation-dependent results for negative numbers. Java removes that uncertainty.

### 3.5.11 Parentheses and Operator Hierarchy

Table 3.4 shows the precedence of operators. If no parentheses are used, operations are performed in the hierarchical order indicated. Operators on the same level are processed from left to right, except for those that are right-associative, as indicated in the table. For example, `&&` has a higher precedence than `||`, so the expression

## 大数据平台技术及应用

本文档介绍大数据平台的核心技术架构与设计思路，涵盖数据采集、存储、计算与可视化等多个层面，为大规模数据处理提供系统化的解决方案。

- 数据采集层：支持多源异构数据的实时采集与传输
- 数据存储层：提供分布式文件存储与NoSQL数据库
- 计算引擎层：支持批处理、流计算与交互式分析
- 数据服务层：提供数据查询、挖掘与可视化能力

| 层次 | 核心组件 | 说明 |
|------|---------|------|
| 采集层 | Flume、Kafka | 日志采集与消息队列 |
| 存储层 | HDFS、HBase | 分布式存储 |
| 计算层 | Spark、Flink | 批流一体计算 |
| 服务层 | Hive、Kylin | 数据仓库与OLAP |

| Operators | Associativity |
|---|---|
| [] . () (method call) | Left to right |
| ! ~ ++ -- + (unary) - (unary) () (cast) new | Right to left |
| * / % | Left to right |
| + - | Left to right |
| << >> >>> | Left to right |
| < <= > >= instanceof | Left to right |
| == != | Left to right |
| & | Left to right |
| ^ | Left to right |
| \| | Left to right |
| && | Left to right |
| \|\| | Left to right |
| ?: | Right to left |
| = += -= *= /= %= &= \|= ^= <<= >>= >>>= | Right to left |

> **C++ NOTE:**
>
> Unlike C or C++, Java does not have a comma operator. However, you can use a *comma-separated list of expressions* in the first and third slot of a for statement.

## 3.6 Strings

Conceptually, Java strings are sequences of Unicode characters. For example, the string `"Java\u2122"` consists of the five Unicode characters J, a, v, a, and ™. Java does not have a built-in string type. Instead, the standard Java library contains a predefined class called, naturally enough, `String`. Each quoted string is an instance of the `String` class:

```java
String e = ""; // an empty string
String greeting = "Hello";
```

### 3.6.1 Substrings

You can extract a substring from a larger string with the `substring` method of the `String` class. For example,

```java
String greeting = "Hello";
String s = greeting.substring(0, 3);
```

creates a string consisting of the characters `"Hel"`.

> **NOTE:**
> Like C and C++, Java counts code units and code points in strings starting with 0.

The second parameter of `substring` is the first position that you *do not* want to copy. In our case, we want to copy positions 0, 1, and 2 (from position 0 to position 2 inclusive). As `substring` counts it, this means from position 0 inclusive to position 3 *exclusive*.

There is one advantage to the way `substring` works: Computing the length of the substring is easy. The string `s.substring(a, b)` always has length b − a. For example, the substring `"Hel"` has length 3 − 0 = 3.

### 3.6.2 Concatenation

Java, like most programming languages, allows you to use + to join (concatenate) two strings.

```java
String expletive = "Expletive";
String PG13 = "deleted";
String message = expletive + PG13;
```

The preceding code sets the variable `message` to the string "Expletivedeleted". (Note the lack of a space between the words: The + operator joins two strings in the order received, *exactly* as they are given.)

When you concatenate a string with a value that is not a string, the latter is converted to a string. (As you will see in Chapter 5, every Java object can be converted to a string.) For example,

```java
int age = 13;
String rating = "PG" + age;
```

sets `rating` to the string "PG13".

This feature is commonly used in output statements. For example,

```java
System.out.println("The answer is " + answer);
```

is perfectly acceptable and prints what you would expect (and with correct spacing because of the space after the word `is`).

If you need to put multiple strings together, separated by a delimiter, use the static `join` method:

```java
String all = String.join(" / ", "S", "M", "L", "XL");
    // all is the string "S / M / L / XL"
```

As of Java 11, there is a `repeat` method:

```java
String repeated = "Java".repeat(3); // repeated is "JavaJavaJava"
```

### 3.6.3 Strings Are Immutable

The String class gives no methods that let you *change* a character in an existing string. If you want to turn greeting into "Help!", you cannot directly change the last positions of greeting into 'p' and '!'. If you are a C programmer, this can make you feel pretty helpless. How are we going to modify the string? In Java, it is quite easy: Concatenate the substring that you want to keep with the characters that you want to replace.

```java
String greeting = "Hello";
greeting = greeting.substring(0, 3) + "p!";
```

This declaration changes the current value of the greeting variable to "Help!".

Since you cannot change the individual characters in a Java string, the documentation refers to the objects of the String class as *immutable*. Just as the number 3 is always 3, the string "Hello" will always contain the code-unit sequence for the characters h,e,l,l,o. You cannot change these values. Yet you can, as you just saw, change the contents of the string variable greeting and make it refer to a different string, just as you can make a numeric variable currently holding the value 3 hold the value 4.

Isn’t that a lot less efficient? It would seem simpler to change the code units than to build up a whole new string from scratch. Well, yes and no. Indeed, it isn’t efficient to generate a new string that holds the concatenation of "Hel" and "p!". But immutable strings have one great advantage: The compiler can arrange that strings are *shared*.

To understand how this works, think of the various strings as sitting in a common pool. String variables then point to locations in the pool. If you copy a string variable, both the original and the copy share the same characters.

Overall, the designers of Java decided that the efficiency of sharing outweighs the inefficiency of string editing by extracting substrings and concatenating. Look at your own programs; most of the time, you probably don’t change strings—you just compare them. (There is one common exception—assembling strings from individual characters or from shorter strings that come from the keyboard or a file. For these situations, Java provides a separate class—see Section 3.6.9, “Building Strings,” on p. 73.)

> **C++ NOTE:**
>
> C programmers are generally bewildered when they see Java strings for the first time because they think of strings as arrays of characters:
>
> ```c
> char greeting[] = "Hello";
> ```
>
> That is a wrong analogy: A Java string is roughly analogous to a char* pointer,
>
> ```c
> char* greeting = "Hello";
> ```
>
> When you replace greeting with another string, the Java code does roughly the following:
>
> ```c
> char* temp = malloc(6);
> strncpy(temp, greeting, 3);
> strncpy(temp + 3, "p!", 3);
> greeting = temp;
> ```
>
> Sure, now greeting points to the string "Help!". And even the most hardened C programmer must admit that the Java syntax is more pleasant than a sequence of strncpy calls. But what if we make another assignment to greeting?
>
> ```c
> greeting = "Howdy";
> ```
