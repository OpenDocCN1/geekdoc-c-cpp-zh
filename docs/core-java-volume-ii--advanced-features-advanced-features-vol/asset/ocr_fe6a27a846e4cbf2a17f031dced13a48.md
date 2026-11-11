```
Listing 12.7 `printf1/Printf1Test.java`

```java
/**
 * @version 1.10 1997-07-01
 * @author Cay Horstmann
 */
class Printf1Test
{
   public static void main(String[] args)
   {
      int count = Printf1.print(8, 4, 3.14);
      count += Printf1.print(8, 4, count);
      System.out.println();
      for (int i = 0; i < count; i++)
         System.out.print("-");
      System.out.println();
   }
}
```
```

# 12.3 String Parameters

Next, let’s look at how to transfer strings to and from native methods. Strings are quite different in the two languages: In Java, they are sequences of UTF-16 code points, whereas C strings are null-terminated sequences of bytes. JNI has two sets of functions for manipulating strings: One converts Java strings to “modified UTF-8” byte sequences and another converts them to arrays of UTF-16 values—that is, to jchar arrays. (The UTF-8, “modified UTF-8,” and UTF-16 formats were discussed in Chapter 2. Recall that the UTF-8 and “modified UTF-8” encodings leave ASCII characters unchanged, but all other Unicode characters are encoded as multibyte sequences.)

> **NOTE:** The standard UTF-8 encoding and the “modified UTF-8” encoding differ only for “supplementary” characters with codes higher than 0xFFFF. In the standard UTF-8 encoding, these characters are encoded as 4-byte sequences. In the “modified” encoding, each such character is first encoded as a pair of “surrogates” in the UTF-16 encoding, and then each surrogate is encoded with UTF-8, yielding a total of 6 bytes. This is clumsy, but it is a historical accident—the JVM specification was written when Unicode was still limited to 16 bits.