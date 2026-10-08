# Chapter 27. Unicode, Wide Characters, And All That

```
char *s = "\u20AC1.23";
```

```
printf("%s\n", s); // €1.23
```

But we are getting into some weirdness, please check this out:

```
char *s = "\u20AC1.23"; // €1.23
```

```
printf("%zu\n", strlen(s)); // 7!
```

The string length of "€1.23" is 7? Yes! Well, on my system, Remember that strlen() returns the number of bytes in the string, not the number of characters. (When we get to "wide characters", coming up, we'll see a way to get the number of characters).

Note that C allows individual multibyte characters (as opposed to char*), the behavior of varies by implementation and your compiler might warn you on.

GCC, for example, of multi-character constants for the following two lines (and, on my system, prints out the UTF-8 encoding):

```
printf("%s\n", '€');
```

```
printf("%s\n", "\u20AC");
```

# 27.7.2 Wide Characters

If you're not a multibyte character, then you're a wide character.

A wide character is a single value that can uniquely represent any character in the current locale. It's analogous to Unicode code points. But it might not. Or it might be.

Basically, multibyte characters are arrays of bytes, wide character strings are arrays of characters. So you can start thinking on a character-by-character basis rather than a byte-by-basis (the latter of which gets messy when characters start taking up varying numbers of bytes).

Wide characters can be represented by a number of types, but the standout is wchar_t. It's the main one. It's like char, except wide.

You might be wondering if it's Unicode or not, and how does allow you so much flexibility in writing code? wchar_t opens some of doors, as there is a rich set of functions you can use with wchar_t (strings like getting the length, etc.) without caring the encoding.

# 27.8 Using Wide Characters and wchar_t

Time for a new turn: wchar_t is this main wide character type. Remember how a char is only one byte? And byte's not enough to represent all characters, potentially? Well, this one is.

To use wchar_t, include <wchar.h>.

How many bytes is it? It's not totally clear. It could be 16 bytes. It could be 32 bytes.

But wait, you're saying—if it's only 16 bytes, it's not enough to hold all the Unicode code points, is it? You right—it's not. The spec doesn't require it to. It just has to be able to represent all the characters in the current locale.

This can cause grief with Unicode on platforms with 16-bit wchar_ts (—Windows). But that's out of scope for this guide.

You can declare a string or character of this type with the l prefix