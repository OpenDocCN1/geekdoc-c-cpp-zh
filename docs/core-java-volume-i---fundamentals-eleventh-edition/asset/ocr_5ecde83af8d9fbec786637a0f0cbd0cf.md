The most common form is a //. Use this for a comment that runs from the // to the end of the line.

```
System.out.println("We will not use 'Hello, World!'"); // is this too cute?
```

When longer comments are needed, you can mark each line with a //, or you can use the /* and */ comment delimiters that let you block off a longer comment.

Finally, a third kind of comment is used to generate documentation automatically. This comment uses a /** to start and a */ to end. You can see this type of comment in Listing 3.1. For more on this type of comment and on automatic documentation generation, see Chapter 4.

# **Listing 3.1** `FirstSample/FirstSample.java`

```
1  /**
2   * This is the first sample program in Core Java Chapter 3
3   * @version 3.01 1997-03-22
4   * @author Gary Cornell
5   */
6  public class FirstSample
7  {
8      public static void main(String[] args)
9      {
10         System.out.println("We will not use 'Hello, World!'");
11     }
12 }
```

> **CAUTION:** `/* */` comments do not nest in Java. That is, you might not be able to deactivate code simply by surrounding it with `/*` and `*/` because the code you want to deactivate might itself contain a `*/` delimiter.

# ### 3.3 Data Types

Java is a strongly typed language. This means that every variable must have a declared type. There are eight primitive types in Java. Four of them are integer types; two are floating-point number types; one is the character type char, used for code units in the Unicode encoding scheme (see Section 3.3.3, “The char Type,” on p. 46); and one is a boolean type for truth values.