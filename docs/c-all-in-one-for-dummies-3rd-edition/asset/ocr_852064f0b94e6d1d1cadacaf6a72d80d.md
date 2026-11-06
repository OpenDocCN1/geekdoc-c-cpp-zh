The *newline* character symbolizes the start of a new line of text. In all cases, the computer places the *insertion point*, the place where it adds new characters, on the next line. If you are printing some text to the console and then you print a newline character, any text that follows will be on the next line. Most compilers these days start the text at the far left end of the next line (Column 1), but some compilers start the text in the next column on the next line, as in the following output. In this case, the text appears on the next line, but it starts at Column 4 rather than at the far left end (Column 1):

```
```
abc
    def
```
```

Here, you print `abc`, and then a newline, and then `def`. Notice that the `def` continues in the same position it would have been had it been on the first line. For the compilers that we use in this book, however, printing `abc`, and then a newline, and finally `def` results in this output:

```
```
abc
def
```
```

But to accommodate the fact that some other compilers sometimes treat a newline as just that (start a new line but don’t go anywhere else), the creators of the computers gave you another special character: the carriage return. (Can you hear the crowd say, “Ooooh!”?)

The *carriage return* places the insertion point at the start of the line, but not on a new line (which means that if you use just a carriage return on a computer expecting both a carriage return and a newline, you overwrite what’s already on the line). That’s true with pretty much every C++ compiler.

In Book I, Chapter 2, we describe the tab character and other characters that start with a backslash. These are individual characters, and you can have them inside a character variable, as in the following example, which prints the letter `a`, and then a tab, and then the letter `b`. Notice that, to get the tab character to go into the character variable, you have to use the `\` and then a `t`:

```
```
char ch = '\t';
cout << "a" << ch << "b" << endl;
```
```

In Book I, Chapter 2, we mention that to put a double quote inside a string, you needed to precede the double quote with a backslash so that the computer won’t think that the double quote is the end of the string. But because a character is surrounded by single quotes, you don’t need to do this: You can just put a double quote inside the character, as in

```
```
char ch = '"';
```
```