Read a character from in into c
Read at most n characters from in into [p:...); consider t a terminator in.get(p,n,'\n')
Read at most n characters from in into [p:...); consider t a terminator; remove terminator from in
in.getline(p,n,'\n')
read at most n characters from in into [p:...)
in.ignore(n) in.ignore(n,traits::eof())
in.ignore() in.ignore(1,traits::eof())
in.swap(in2) Exchange the values of in and in2

If you have a choice, use formatted input (§38.4.1.1) instead these low-level input functions. The simple get(c) is useful when you need to compose your values out of characters. The other get() function and getline() read sequences of characters into a fixed-size area [p:...). They read until they reach the maximum number of characters or find their terminator character (by default '\n'). They place a 0 at the end of the characters (if any) written to; getline() removes its terminator from the input, if found, whereas get() does not. For example:

```
void f() // low-level, old-style line read {
char word[MAX_WORD][MAX_LINE]; // MAX_WORD arraysofMAX_LINE char each
int i = 0;
while(cin.getline(word[i++],MAX_LINE,'\n') && i<MAX_WORD)
/* do nothing*/ ;
// ...
}
```

For these functions, it is not immediately obvious what terminated the read:

+   - We found the terminator.
+   - We read the maximum number of characters.
+   - We hit end-of-file.
+   - There was a non-format input error.

The last two alternatives are handled by looking at the file state (§38.3). Typically, the appropriate actions are quite different for these cases.

A read(p,n) does not write a 0 to the array after the characters read. Obviously, the formatted input operators are simpler to use and less error-prone than the unformatted ones.

The following functions depend on the detailed interaction between the stream buffer (§38.6) and the real data source and should be used only if necessary and then very carefully:

# Unformatted Input (§iso.27.7.2.3)

x=in.peek() x is the current input character; x is not extracted from in’s stream buffer and will be the next character read
n=in.readsome(p,n) If rdbuf()->in_avail()==-1, call setstate(eofbit); otherwise read at