troubles.” Fortunately, sanity prevailed. The Java launcher in Java 1.4 and beyond enforces that the `main` method is public.

Of course, it is frustrating to have quality assurance engineers, who are often overworked and not always experts in the fine points of Java, make questionable decisions about bug reports. But it is remarkable that the bug reports and their resolutions have been available for anyone to scrutinize, long before Java was open source.

Notice the braces `{ }` in the source code. In Java, as in C/C++, braces delineate the parts (usually called *blocks*) in your program. In Java, the code for any method must be started by an opening brace `{` and ended by a closing brace `}`.

Brace styles have inspired an inordinate amount of useless controversy. This book follows a style that lines up matching braces. As whitespace is irrelevant to the Java compiler, you can use whatever brace style you like.

For now, don’t worry about the keywords `static void`—just think of them as part of what you need to get a Java program to compile. By the end of Chapter 4, you will understand this incantation completely. The point to remember for now is that every Java application must have a `main` method that is declared in the following way:

```
```java
public class ClassName
{
    public static void main(String[] args)
    {
        program statements
    }
}
```
```

![](bbox=[0.128, 0.832, 0.181, 0.873])

# **C++ NOTE:**