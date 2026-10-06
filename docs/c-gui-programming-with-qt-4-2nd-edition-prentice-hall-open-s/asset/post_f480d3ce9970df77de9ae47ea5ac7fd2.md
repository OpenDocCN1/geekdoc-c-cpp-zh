
it is a superset of ASCII). The XML format is an interesting example of this. The XML files are normally encoded as UTF-8 or UTF-16. The proper way to read them is to call setCodec() with "UTF-8". If the format is UTF-16, QStream will automatically detect it and adjust itself. The <?xml?> header of an XML file sometimes contains an encoding argument, for example:

```
<xml version="1.0" encoding="EUC-KR"?>
```

Since QStream doesn't allow you to change the encoding once it has started, the right way to respect an explicit encoding is to start reading the file afresh, using the QTextCodec::codecForName()). In the case of XML, we can avoid handling the encoding ourselves by using Qt's classes, described in Chapter 16.

Another use of QTextCodecs is to specify the encoding of strings that occur in the source code. Let's consider, for example, a team of Japanese programmers who are writing an application targeted at Japan's home market. The programmers are likely to write their source code in a text editor that uses an encoding such as EUC-JP or Shift-JIS. Such an editor allows them to type in Japanese characters seamlessly so that they can write code like:

```
QPushButton *button = new QPushButton(tr("ボタン"));
```

By default, Qt interprets arguments to tr() as Latin-1. To change this, call the QTextCodec::codecForTr() static function. For example:

```
QTextCodec::codecForTr(QTextCodec::codecForName("EUC-JP"));
```

This must be done before the first call to tr(). Typically, we would do this in main(), immediately after the QCoreApplication or QApplication object is created.

Other strings specified in the program will still be Latin-1 strings. If the programmers want to enter Japanese characters in those as well, they can explicitly convert them to Unicode using a QTextCodec:

```
QString text = japaneseCodec->toUnicode("日本語語理");
```

Alternatively, they can tell Qt to use a specific codec when converting between const char * and QString by calling QTextCodec::setCodecForCStrings():

```
QCodec::codecForCStrings(QCodec::codecName("EUC-JP"));
```

The techniques described above can be applied to any non-Latin-1 language, including Chinese, Greek, Korean, and Russian.

Here's a list of the encodings supported by Qt 4.3:

- Apple Roman
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
- WINSAMI2

For all of these, `QTextCodec::codecName()` will always return a valid pointer.
Other encodings can be supported by subclassing `QTextCodec`.

# Part III: Advanced Qt

# 18. Internationalization

![](img/5a524abdf0b0d58fa99d30abb4463611_672_0.png)

- Working with Unicode
- Making Applications Translation-Aware
- Dynamic Language Switching
- Translating Applications

In addition to the Latin alphabet used for English and for many European languages, Qt 4 also provides extensive support for the rest of the world's writing systems:

- Qt uses Unicode throughout the API and internally. No matter what language we use for the user interface, the application can support all users alike.
- Qt's text engine can handle all the major non-Latin writing systems, including Arabic, Chinese, Cyrillic, Hebrew, Japanese, Korean, Thai, and the Indic languages.
- Qt's layout engine supports right-to-left layouts for languages such as Arabic and Hebrew.
- Certain languages require special input methods for entering text. Editor widgets such as QLineEdit and QTextEdit work well with any input method installed on the system.

Often, isn't enough to allow users to enter text in their native language; the entire user interface must be translated as well. Qt makes this easy: Simply wrap all visible strings with tr() function (as we have done in earlier chapters) and use Qt's tools to prepare translation files in the required languages. Qt provides a GUI tool called Linguist for translators. Linguist is complemented by two command-line programs, update and lrelease, which are typically run by the application's developers. For most applications, a translation file is loaded at startup. But in a few cases, it is also necessary for users to be able to switch languages at-time. This is perfectly possible with Qt, although it requires extra work. And thanks to Qt's layout system, the various user interface components will automatically adjust to make room for translated texts when they are longer than the original.

# Working with Unicode

Unicode is a character encoding standard that supports most of the world's writing systems. The original idea behind Unicode is that using 16 bits for storing characters instead of 8 would be possible to encode around 65535 characters. These characters can be represented using sequences of two 16-bit values called "surrogate pairs".

Qt's QString stores strings as Unicode. Each character in a QString is 16-bit rather than 8-bit char. Here are two ways of setting the first character of a string to 'A':

```
str[0] = 'A';
str[0] = QChar(0x41);
```

If the source file is encoded in Latin-1, specifying Latin-1 characters is just easy:

```
str[0] = 'A';
```

And if the source file has another encoding, the numeric value works fine:

```
str[0] = QChar(0xD1);
```

We can specify any Unicode character by its numeric value. For example, here's how to specify the Greek letter sigma ('Σ') and the euro currency symbol ('€'):

```
str[0] = QChar(0x3A3);
str[0] = QChar(0x2AC);
```

The numeric values of all the characters supported by Unicode are listed at http://www.unicode.org/standard/. If you rarely need non-Latin-1 Unicode, looking up characters is sufficient; but Qt provides convenient ways of entering Unicode strings in a Qt program, as we will see later in this section.

Qt 4's text engine supports the following writing systems on all platforms: Arabic, Chinese, Cyrillic, Hebrew, Japanese, Korean, Lao, Latin, Thai, and Vietnamese. It also supports all the Unicode scripts that don't require special processing. In addition, the following writing systems are supported on X11 with Fontconfig and on recent versions of Windows: Bengali, Devanagari, Gujarati, Gurmuk, Kannada, Khmer, Malayalam, Syriac, Tamil, Telugu, Thaana (Dhivehi), and Tibetan. Finally, Oriya is supported on X11, and Mongolian and Sinhala are supported on Windows. Assuming that the proper fonts are installed on the system, Qt can render text using any of these writing systems. And assuming that the proper input methods are installed, users will be able to enter text in their Qt applications.

Programming with QChar is slightly different from programming with char. To obtain the value of a QChar call unicode() on. To obtain the ASCII or Latin-1 value of a QChar (as a char) call toLatin1(). For non-Latin-1 characters, toLatin1() returns '\0'.

If we know all the strings in a program are ASCII, we can use standard <cctype> functions to guess as isalpha(), isdigit(), and isspace() on the return value of tolatin1(). However, it is generally better to use QChar's member functions for performing these operations, since they will work for any Unicode character. The functions QChar provides is isPrint(), isPunct(), isSpace(), isMark(), isLetter(), isNumber(), isLetterOrNumber(), isDigit(), isSymbol(), isLower(), and isUpper(). For example, here's one way to test that a character is a digit or uppercase letter:

```
if (ch.isdigit() || ch.isUpper())
...
```

The code snippet for every alphabet that distinguishes between uppercase and lowercase, including Latin, Greek, and Cyrillic.

Once we have a Unicode string, we can use it anywhere in Qt's API where a QString is expected. It is then Qt's responsibility to display it properly and to convert it to the relevant encodings when talking to the operating system.

Special care is needed when we read and write files. Text files can use a variety of encodings, and it is often impossible to guess a text file's encoding from its contents. By default, QTextStream uses the system's local 8-bit encoding (available as QText::encodeForLocale()) for both reading and writing. For American and Western locales, this usually means Latin-1.
