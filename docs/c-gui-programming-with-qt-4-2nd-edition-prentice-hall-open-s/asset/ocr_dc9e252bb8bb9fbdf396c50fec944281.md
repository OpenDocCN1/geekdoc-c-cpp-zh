We design our own file format and want to be able to read and write arbitrary Unicode characters, we can save the data as Unicode calling
stream.setCodec("UTF-16");
stream.setGenerateByteMark(true);

before writing to a QText. The data will be saved in UTF-16, a format that requires two bytes per character, and will be prefixed with a 16-bit value (the Unicode order mark, 0xFFFF) identifying that the file is in Unicode and whether the bytes are little-endian or big-endian. The UTF-16 format is identical to the memory representation of a QString, so reading and writing Unicode strings in UTF-16 can be very fast. On the other hand, there is no inherent overhead when saving ASCII in UTF-16 format, since it stores two bytes for every character instead of just one.

Other encodings can be specified by calling codec() on QTextCodec. A is an object that converts between Unicode and encoding. It uses QTextCodecs in a variety of contexts. Internally, they are used to support fonts, input methods, the clipboard, drag and drop, and file names. But they are also available to us when we use Qt applications.

When reading a text file, QTextStream detects UTF-16 automatically if the file starts with the byte order mark. This behavior can be turned off by calling autoDetectUnicode(false). If the data is UTF-16 but can't be assumed to start with the byte order mark, it is best to call codec() with "UTF-16" before reading.

Another encoding that supports the world of Unicode is UTF-8. Its main advantage over UTF-16 is that it is a superset of ASCII. Any character in the range 0x00 to 0x7F is represented as a single byte. Other characters, Latin-1 characters above 0x7F, are represented by multi-byte sequences. For text that is mostly ASCII, UTF-8 takes about half the space consumed by UTF-16. To use UTF-8 with QTextStream, setCodec("UTF-8") as the codec name before reading and writing.

If we want to read and write regardless of the user's locale, we can set the ISO 8859-1 codec on the QTextStream. For example:

```
QTextStream in(&file);
setCodec("ISO 8859-1");
```

Some formats specify their encoding in their header. The header is typically ASCII to ensure that it is read correctly no matter what encoding is used