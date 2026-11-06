```
```python
>>> print ('I am a single quoted string')
I am a single quoted string
>>> print ("I am a double quoted string")
I am a double quoted string
>>> print ("""I am a triple quoted string""")
I am a triple quoted string
```
```

As you can see, quotation marks start and end strings. By default, Python will consider the quotation marks in your statements as markers for the beginning or end of strings.

In some situations, however, you have to include quotation marks in your statements. That means you must stop Python from ending your statements prematurely (i.e. when it sees the quotation marks in your codes). You can accomplish this using a backslash. By adding a backslash right before the quotation marks, you’re telling Python that those marks are included in the string. The act of putting a backslash before a different symbol is known as “escaping” that particular symbol.

Important Note: When adding a backslash to your Python strings, you still need to “escape” it (i.e. place a backslash before the needed backslash). This action will inform Python that the backslash must be used as an ordinary symbol. Analyze the screenshot below:

```
```python
>>> print ("So I said, \"You don't know me! You'll never understand me!\"")
So I said, "You don't know me! You'll never understand me!"
>>> print ('So I said, "You don\'t know me! You\'ll never understand me!"')
So I said, "You don't know me! You'll never understand me!"
>>> print ("This will result in only three backslashes: \\ \\ \\")
This will result in only three backslashes: \ \ \
>>> print ("""The double quotation mark (") is used to indicate direct quotations.""")
The double quotation mark (") is used to indicate direct quotations.
```
```

After analyzing the examples above, you’ll realize that only the characters used to quote strings must be escaped. This simple rule makes Python statements easy to read.

To help you understand strings further, let’s visit your first Python program:

```
```python
>>> print("Hello, world!")
Hello, world!
```
```

Well, it seems you have used strings even before you learned about them. You may also concatenate strings in the Python programming language. Concatenation is the process of