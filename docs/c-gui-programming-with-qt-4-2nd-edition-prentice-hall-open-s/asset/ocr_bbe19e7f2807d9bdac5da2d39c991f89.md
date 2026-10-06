file formats, a full-blown parser may be required. Such might work by reading the data character by using >> QChar, by line, using QTextStream::readLine(). At this end of this section, we present two small examples, one that reads an input line by line, and another that reads it by character. For parsers that work on text, we could read the complete file in one go using QTextStream::readAll() if we are not concerned about memory usage, or if we know the file will be

By default, QTextStream uses the system's local encoding (e.g., ISO 8859-1 or ISO 8859-15 in America and much of Europe) for reading and writing. This can be changed using setCodec() as follows:

```
stream.setCodec("UTF-8");
```

The UTF-8 encoding used in the example is a ASCII-compatible encoding that can represent the entire Unicode character set. For more information about Unicode and QTextStream's supports for encoding, Chapter 18.

QTextStream has various options modeled after those offered by <iostream>. These can be set by passing special objects, called stream manipulators, on the stream to alter its state, or by calling the functions listed in Figure 12.1. The following example sets the showcase, uppercasedigit, and hex options before it outputs the integer 12345678, producing the text "0xBC614E":

```
out << showcase << uppercasedigit << hex << 12345678;
```

# Figure 12.1. Functions to set QTextStream's options

| | Auto-detected based on prefix (when reading) |
|---|---|
| 0 | |
| 2 | Binary |
| 8 | Octal |
| 10 | Decimal |
| 16 | Hexadecimal |

| setNumberFlags(NumberFlags) |
|---|