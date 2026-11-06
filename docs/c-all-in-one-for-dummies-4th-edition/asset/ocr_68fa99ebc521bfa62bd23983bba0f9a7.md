And finally, to put a backslash inside a character, you use two backslashes:

```
`char ch = '\\';`
```

![](bbox=[0.174, 0.166, 0.239, 0.233])

When the compiler sees a backslash inside a string or a character, it treats the backslash as special and looks at whatever follows it. If you have something like `'\'` with no other character inside the single quotes following it, the compiler thinks the final quote is to be combined with the backslash. And then it moves forward, expecting a single quote to follow, representing the end. Because a single quote doesn’t appear, the compiler gets confused and issues an error. Compilers are easily confused — kind of gives you more respect for the human brain.

# CARRIAGE RETURN, NEWLINE, OR BOTH?

Depending on what platform you use (such as Windows, Linux, or Mac) and on which applications you use, the effect of the carriage return, newline, or a combination of both varies. In some cases, it’s really enough to drive you quite nuts. The form that seems to work best in all situations is the combination of the carriage return and linefeed (\r\n). Sometimes, you can also use the linefeed and carriage return combination (\n\r), but oddly enough, it doesn’t always produce the same result as \r\n. Here is a quick sampling based on platform:

+   - **Windows:** `\r\n`
+   - **Linux:** `\n`
+   - **Older Mac:** `\r`
+   - **Acorn BBC and RISC:** `\n\r`

This list doesn’t even get into the domain of mainframes and other computers, which can use very odd combinations like \025. Sometimes a single character doesn’t produce any result at all. For example, when working with Windows Notepad, you must provide the \r\n combination because using \n alone won’t do anything. However, when importing a file using some C++ libraries, all you want is the \n because the library will see the \r as a second line. This is the reason that many developers use just \n, which, as previously mentioned, doesn’t show up in some editors.

So, there isn’t a pat answer to the question of which character to use, and you need to experiment to ensure that using \r, \n, \r\n, or \n\r will actually work the way you want it to in the situation you’re dealing with. When in doubt, rely on \r\n until you know that the combination won’t work.