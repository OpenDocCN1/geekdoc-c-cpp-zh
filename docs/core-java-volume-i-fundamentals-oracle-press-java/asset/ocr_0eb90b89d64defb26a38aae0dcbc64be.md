Text blocks are particularly suited for including code in some other language, such as SQL or HTML. You can just paste it between the triple quotes:

```
```
String html = """
<div class="Warning">
    Beware of those who say "Hello" to the world
</div>
""";
```
```

Note that you don’t have to escape the quotation marks. There are just two situations where you need to escape them:

+   * If the text block *ends* in a quotation mark
+   * If the text block contains a sequence of three or more quotation marks

Unfortunately, you still need to escape all backslashes.

All escape sequences from regular strings work the same way in text blocks.

There is one escape sequence that only works in text blocks. A \ directly before the end of a line joins this line and the next. For example,

```
```
"""
Hello, my name is Hal. \
Please enter your name: """;
```
```

is the same as

```
```
"Hello, my name is Hal. Please enter your name: "
```
```

Line endings are normalized by removing trailing whitespace and changing any Windows line endings (\r\n) to simple newlines (\n). In the unlikely case that you need to preserve trailing spaces, turn the last one into a \s escape.