# Chapter 27. Unicode, Wide Characters, and All That

Look in for the patterns. Note that UTF-16BE and UTF-32BE are simply the code point represented as 16- and 32-bit values.

Little-endian is the same, the bytes are in little-endian order.

Then we have UTF-8 at the first. You might notice that the single-byte code points are represented as a single byte. You might also notice that different code points take different number of bytes. This is a variable-width encoding.

So as soon as we get above a certain value, UTF-8 starts using bytes to store the values. And they don't appear to correlate with the code point value.

The details of UTF-8 encoding are beyond the scope of this guide, but it's enough to know that it has a variable number of bytes per code point, and those bytes don't match the code point for the first 128 code points. If you really want to learn more, Computerfile has a great UTF-8 video with Tom Scot.

That last is a bit about Unicode and UTF-8 from a North American perspective: it's backward compatible with 7-bit ASCII encoding; If you're used to ASCII, UTF-8 is the same! Every ASCII-encoded document is also UTF-8 encoded! (But not the other way around, obviously.)

It's possibly more than any that is driving UTF-8 to take the world.

# 27.4 Source and Execution Character Sets

When programming in C, there are (at least) three character sets that are in:

+   * The one your code exists as.
* The one the compiler translates into as compilation begins (the source character set). This might be the same as the one, or it might not.
* The one the compiler translates the source character into execution (the execution character set). This might be the same as the source character set, or it might not.

Your compiler probably has options to select these character sets at build-time.

The basic character set for both source and execution will contain the following characters:

```
A B C D E F G H I J K L M
OP Q R S T U V W X Y Z
a b c d e f g h i j k l m
p q r s t u v w x y z
0 1 2 3 4 5 6 7 8 9
! " % & ( ) * + , - /
;< = ? [ \ ] ^ . |
space tab vertical-tab end-of-line
form-feed
```

Those are the characters you can use in your source and remain 100 percent.

The execution character set will have additional characters for alert (bell/flash), backspace, carriage return, and newline.

But most people don't go to that and freely use their extended character sets in source and executable, especially now that Unicode and UTF-8 are getting more common. I mean, the basic character set doesn't even allow for €, $, or !

> 6Again, this is only true in UTF-16 for characters that fit in two bytes.

> 7https://en.wikipedia.org/wiki/UTF-8

> 8https://www.youtube.com/watch?v=MjmeeoH9LT4