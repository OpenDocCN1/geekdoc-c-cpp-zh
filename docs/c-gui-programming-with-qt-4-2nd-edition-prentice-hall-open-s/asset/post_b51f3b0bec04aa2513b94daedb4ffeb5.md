
we design our own file format and want to be able to read and write arbitrary
Unicode characters, we can save the data as Unicode by calling
```cpp
stream.setCodec("UTF-16");
stream.setGenerateByteOrderMark(true);
```
before we writing to a QTextStream. The data will be saved in UTF-16,
a format that requires two bytes per character, and will be prefixed with a special
16-bit value (the Unicode order mark, 0xFFFF) identifying that the file is in
Unicode and whether the bytes are little-endian or big-endian. The UTF-16
format is identical to the memory representation of a QString, so reading and
writing Unicode strings in UTF-16 can be very fast. On the other hand, there is an
other overhead when saving ASCII in UTF-16 format, since it stores
two bytes for every character instead of just one.

Other encodings can be specified by calling setCodec(). QCodec::TTextCodec is an object that converts Unicode and a given
encoding. It uses QTextCodes in a variety of contexts. Internally, they are used
to support fonts, input methods, the clipboard, drag and drop, and file names. But
they are also available to us when we use Qt applications.

When reading a text file, QTextStream detects UTF-16 automatically if the file
starts with the byte order mark. This behavior can be turned off by calling
setAutoDetectUnicode(false). If the data is UTF-16 can't be assumed to
start with the byte order mark, it is best to call setCodec("UTF-16") before
reading.

Another encoding that supports the whole of Unicode is UTF-8. Its main advantage
over UTF-16 is that it is a superset of ASCII. Any character in the range 0x00
0x7F is represented as a single byte. Other characters, Latin-1 characters
0x80-0xFF, are represented by multi-byte sequences. For text that is mostly ASCII,
UTF-8 takes about half the space consumed by UTF-16. To use UTF-8 with
TextStream, setCodec("UTF-8") as the codec name before reading and
writing.

If we want to read and write UTF-8 regardless of the user's locale, we can
set the ISO 8859-1 codec on the QTextStream. For example:

```cpp
QTextStream in(&file);
in.setCodec("ISO 8859-1");
```

Some formats specify their encoding in their header. The header is typically
ASCII to ensure that it is read correctly no matter what encoding is used
that it is a superset of ASCII. The XML file format is an interesting example of this. XML files are normally encoded as UTF-8 or UTF-16. The proper way to read them is to call setCodec() with "UTF-8". If the format is UTF-16, QStream will automatically detect it and adjust itself. The <?xml?> header of an XML file contains an encoding argument, for example:

```xml
<xml version="1.0" encoding="EUC-KR">
```

Since QTextStream doesn't allow you to change the encoding once it has started, the right way to respect an explicit encoding is to start reading the file afresh, using the correct QTextCodec (obtained from QTextCodec::codecForName()). In the case of XML, we can avoid handling the encoding ourselves by using Qt's classes, described in Chapter 16.

Another use of QTextCodecs is to specify the encoding of strings that occur in the source code. Let's consider, for example, a team of Japanese programmers who are writing an application targeted at the Japan's market. These programmers are likely to write their source code in a text editor that uses an encoding such as EUC-JP or Shift-JIS. Such an editor allows them to type in Japanese characters seamlessly so that they can write code like:

```cpp
QPushButton *button = new QPushButton(tr("日本語"));
```

By default, Qt interprets arguments to tr() as Latin-1. To change this, call the QTextCodec::codecForTr() static function. For example:

```cpp
QTextCodec::codecForTr(QTextCodec::codecForName("EUC-JP"));
```

This must be done before the first call to tr(). Typically, we would do this in main(), immediately after the QCoreApplication or QApplication object is created.

Other strings specified in the program will still be interpreted as Latin-1 strings. If the programmers want to enter Japanese characters in those as well, they can explicitly convert them to Unicode using a QTextCodec:

```cpp
QString text = japaneseCodec->toUnicode("日本語");
```

Alternatively, they can tell Qt to use a specific codec when converting between const char * and QString by calling QTextCodec::setCodecForCStrings():

```cpp
QCodec::setCodecForStrings(QCodec::codecName("EUC-JP"));
```

The techniques described above can be applied to any non-Latin-1 language, including Chinese, Greek, Korean, and Russian.

Here's a list of the encodings supported by Qt 4.3:

-- Apple Roman
- Big5
- Big5-HKSCS
- EUC-JP
- EUC-KR
- GB18030-0
- IBM 850
- IBM 866
- IBM 874
- ISO 2022-JP
- ISO 8859-1
- ISO 8859-2
- ISO 8859-3
- ISO 8859-4
- ISO 8859-5
- ISO 8859-6
- ISO 8859-7
- ISO 8859-8
- ISO 8859-9
- ISO 8859-10
- ISO 8859-13
- ISO 8859-14
- ISO 8859-15

# ISO 8859-16

- Ascii-Bng
- Ascii-Dev
- Ascii-Gjr
- Ascii-Knd
- Ascii-MLM
- Ascii-Ori
- Ascii-Pnj
- Ascii-Tlg
- Ascii-Tml
- JIS X 0201
- JIS X 0208
- KOI8-R
- KOI8-U
- MuleLao-1
- ROMAN8
- Shift-JIS
- TIS-620
- TSCII
- UTF-8
- UTF-16
- UTF-16BE
- UTF-16LE
- Windows-1250
- Windows-1251
- Windows-1252
- Windows-1253
- Windows-1254
- Windows-1255
- Windows-1256
- Windows-1257
- Windows-1258
- Windows-1259
