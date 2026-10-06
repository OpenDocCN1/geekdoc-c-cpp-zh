# Strings, Byte Arrays, and Variants

QString, QByteArray, and QVariant are three classes that have many things in containers that can be used as alternatives to containers in some contexts. Also, like the containers, these classes use implicit sharing a memory and speed optimization.

We will start with QString. Every GUI program uses strings, not only for the user interface but also as data structures. C++ natively provides two kinds of strings: traditional C-style '\0'-terminated character arrays and std::string class. Unlike these, QString holds 16-bit Unicode characters. Unicode contains ASCII and Latin-1 as a subset, but since 16-bit, it represents thousands of other characters for writing most of the world's languages. See Chapter 18 for more information about Unicode.

When using QString, we don't need to worry about arcane details of allocating memory or ensuring that the data is '\0'-terminated. Conceptually, QStrings can be thought of as a vector of QChars. A QString can easily embed '\0' characters. The length() function returns the size of the entire string, including embedded '\0' characters.

QString provides a binary + to concatenate two strings and a += operator to append one string to another. Because QString automatically preallocates memory at the end of the string data, building up a string by repeatedly appending characters is very fast. Here's an example that combines + and +=:

```
QString str = "User: ";
str += userName + "\n";
```

There is also a QString::append() function that does the same thing as the += operator:

```
str = "User: ";
str.append(userName);
str.append("\n");
```

A completely different way to combine strings is to use QString's sprintf() function:

```
str.sprintf("%s %.1f%%", "perfect competition", 100.0);
```

This function supports the same format specifiers as the C++ library's sprintf() function. In the preceding example, str is assigned "perfect competition 100.0%%".