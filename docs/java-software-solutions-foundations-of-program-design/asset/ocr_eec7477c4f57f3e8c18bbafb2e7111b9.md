# Characters

Characters are another fundamental type of data used and managed on a computer. Individual characters can be treated as separate data items, and, as we’ve seen in several examples, they can be combined to form character strings.

A *character literal* is expressed in a Java program with single quotes, such as 'b' or ']' or ';'. You will recall that *string literals* are delineated using double quotation marks, and that the `String` type is not a primitive data type in Java; it is a class name. We discuss the `String` class in detail in the next chapter.

Note the difference between a digit as a character (or part of a string) and a digit as a number (or part of a larger number). The number 602 is a numeric value that can be used in an arithmetic calculation. But in the string "602 Greenbriar Court" the 6, 0, and 2 are characters, just like the rest of the characters that make up the string.

The characters we can manage are defined by a *character set*, which is simply a list of characters in a particular order. Each programming language supports a particular character set that defines the valid values for a character variable in that language. Several character sets have been proposed, but only a few have been used regularly over the years. The *ASCII character set* is a popular choice. ASCII stands for the American Standard Code for Information Interchange. The basic ASCII set uses seven bits per character, providing room to support 128 different characters, including:

+   - uppercase letters, such as 'A', 'B', and 'C'
+   - lowercase letters, such as 'a', 'b', and 'c'
+   - punctuation, such as the period ('.'), semicolon (';'), and comma (',')
+   - the digits '0' through '9'
+   - the space character, ' '
+   - special symbols, such as the ampersand ('&'), vertical bar ('|'), and backslash ('\\')
+   - control characters, such as the carriage return, null, and end-of-text marks

The *control characters* are sometimes called nonprinting or invisible characters because they do not have a specific symbol that represents them. Yet they are as valid as any other character and can be stored and used in the same ways. Many control characters have special meaning to certain software applications.

As computing became a worldwide endeavor, users demanded a more flexible character set containing other language alphabets. ASCII was extended to use eight bits per character, and the number of characters in the set doubled to 256. The extended ASCII contains many accented and diacritical characters used in languages other than English.

![](bbox=[0.687, 0.833, 0.951, 0.904])