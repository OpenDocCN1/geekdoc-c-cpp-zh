# Accepting Keyboard Input

> CAUTION
getch() is not an ANSI-Standard command, but many C compilers support it.

# The getc() and fgetc() Functions

The getc() and fgetc() character input functions don't automatically work with stdin. Instead, they let the program specify the input stream. They are used primarily to read characters from disk files. See Lesson 17 for more details.

| DO | DON'T |
|---|---|
| understand the difference between echoed and unechoed input. | DON'T use non-ANSI Standard functions if portability is a concern.
| understand the difference between buffered and unbuffered input. | DON'T expect non-ANSI Standard functions to work the same if you switch compilers.|

# “Ungetting a Character with ungetc”

What does ungetting a character mean? An example should help you understand. Suppose your program reads characters from an input stream many. For example, you might input digits only, so you know that input has ended when the first nondigit character is encountered. That first nondigit character might be an important part of subsequent data, but it has been removed from the input stream. Is it lost? No, it can be “ungotten” or returned to the input stream, where it is the first character read by the next input operation on that stream.

To “unget” a character, you use ungetc() library function. Its prototype is `int ungetc(int ch, FILE *fp);`

The argument ch is the character to be returned. The argument *fp specifies the stream that the character is to returned to, which can be any input stream. For now, specify stdin as the second argument: ungetc(ch, stdin); The notation *fp is used with streams associated with disk files; you learn about this in Lesson 17.

You can unget only a single character to a stream between reads, and you can’t unget at any time. The function ungetc() returns ch on success and EOF if the character can’t be returned to the stream.