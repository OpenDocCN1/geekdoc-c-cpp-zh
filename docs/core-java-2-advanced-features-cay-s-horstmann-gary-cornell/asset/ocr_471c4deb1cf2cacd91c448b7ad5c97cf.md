```
~~~java
67  String line = in.nextLine();
68  String[] tokens = line.split("\\s+");
69  String name = tokens[0];
70  double salary = Double.parseDouble(tokens[1]);
71  LocalDate hireDate = LocalDate.parse(tokens[2]);
72  int year = hireDate.getYear();
73  int month = hireDate.getMonthValue();
74  int day = hireDate.getDayOfMonth();
75  return new Employee(name, salary, year, month, day);
76  }
77  }
~~~
```

# 2.2.4 Character Encodings

Input and output streams are for sequences of bytes, but in many cases you will work with texts—that is, sequences of characters. It then matters how characters are encoded into bytes.

Java uses the Unicode standard for characters. Each character or “code point” has a 21-bit integer number. There are different character encodings—methods for packaging those 21-bit numbers into bytes.

The most common encoding is UTF-8, which encodes each Unicode code point into a sequence of one to four bytes (see Table 2.1). UTF-8 has the advantage that the characters of the traditional ASCII character set, which contains all characters used in English, only take up one byte each.

Table 2.1 UTF-8 Encoding

| Character Range | Encoding |
|---|---|
| 0…7F | 0xxxxxxx |
| 80…7FF | 110xxxxx 10xxxxxx |
| 800…FFFF | 1110xxxx 10xxxxxx 10xxxxxx |
| 10000…10FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx |

Another common encoding is UTF-16, which encodes each Unicode code point into one or two 16-bit values (see Table 2.2). This is the encoding used in Java strings. Actually, there are two forms of UTF-16, called “big-endian” and “little-endian.” Consider the 16-bit value 0x2122. In big-endian format, the more significant byte comes first: 0x21 followed by 0x22. In little-endian format, it is the other way around: 0x22 0x21. To indicate which of the two is used, a file can start with the “byte order mark,” the 16-bit quantity 0xFEFF. A reader can use this value to determine the byte order and discard it.