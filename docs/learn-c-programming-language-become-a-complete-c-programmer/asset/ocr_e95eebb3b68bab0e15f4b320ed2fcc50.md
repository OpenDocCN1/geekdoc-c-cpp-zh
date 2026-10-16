Raw string literals use the R"(ccc)" notation for a sequence of characters ccc. The initial R is there to distinguish raw string literals from ordinary string literals. The parentheses are there to allow (“unescaped”) double quotes. For example:

```
R"("quoted string")" // the string is "quoted string"
```

So, how do we get the character sequence )" into a raw string literal? Fortunately, that’s a rare problem, but "( and )" is only the default delimiter pair. We can add delimiters before the ( and after the ) in "(...)". For example:

```
R"***("quoted string containing the usual terminator (")")***"
// "quoted string containing the usual terminator (")"
```

The character sequence after the ) must be identical to the sequence before the (. This way we can cope with (almost) arbitrarily complicated patterns.

Unless you work with regular expressions, raw string literals are probably just a curiosity (and one more thing to learn), but regular expressions are useful and widely used. Consider a real-world example:

```
"('(?:[^\\]|\.)*|' (?:[^\\]|\.)*')" // Are the fivebackslashes correct or not?
```

With examples like that, even experts easily become confused, and raw string literals provide a significant service.

In contrast to nonraw string literals, a raw string literal can contain a newline. For example:

```
string counts {R"(1
22
333)"};
```

is equivalent to

```
string x {"1\n22\n333"};
```

# 7.3.2.2 Larger Character Sets

A string with the prefix L, such as L"angst", is a string of wide characters (§6.2.3). Its type is const wchar_t[]. Similarly, a string with the prefix LR, such as LR"(angst)", is a raw string (§7.3.2.1) of wide characters of type const wchar_t[]. Such a string is terminated by a L'\0' character.

# Section 7.3.2.2 Larger Character Sets 179

There are six kinds of character literals supporting Unicode ( Unicode literals). This sounds excessive, but there are three major encodings of Unicode: UTF-8, UTF-16, and UTF-32. For each of these three alternatives, both raw and “ordinary” strings are supported. All three UTF encodings support all Unicode characters, so which you use depends on the system you need to fit into. Essentially all Internet applications (e.g., browsers and email) rely on one or more of these encodings.

UTF-8 is a variable-width encoding: common characters fit into 1 byte, less frequently used characters (by some estimate of use) into 2 bytes, and rarer characters into 3 or 4 bytes. In particular, the ASCII characters fit into 1 byte with the same encodings (integer values) in UTF-8 as in ASCII. The various Latin alphabets, Greek, Cyrillic, Hebrew, Arabic, and more fit into 2 bytes.