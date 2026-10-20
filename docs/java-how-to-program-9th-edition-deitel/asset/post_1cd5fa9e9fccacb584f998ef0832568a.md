
| Operator | Description | Associativity |
|---|---|---|
| | | bitwise inclusive OR |
| boolean logical inclusive OR | left to right |
| && | conditional AND | left to right |
| || | conditional OR | left to right |
| ?: | conditional | right to left |
| = | assignment | right to left |
| += | addition assignment |  |
| -= | subtraction assignment |  |
| *= | multiplication assignment |  |
| /= | division assignment |  |
| %= | remainder assignment |  |
| &= | bitwise AND assignment |  |
| ^= | bitwise exclusive OR assignment |  |
| |= | bitwise inclusive OR assignment |  |
| <<= | bitwise left-shift assignment |  |
| >>= | bitwise signed-right-shift assignment |  |
| >>>= | bitwise unsigned-right-shift assignment |  |

Fig. A.1 | Operator precedence chart. (Part 2 of 2.)

## ASCII Character Set

|  | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 | nul | soh | stx | etx | eot | enq | ack | bel | bs | ht |
| 1 | nl | vt | ff | cr | so | si | dle | dc1 | dc2 | dc3 |
| 2 | dc4 | nak | syn | etb | can | em | sub | esc | fs | gs |
| 3 | rs | us | sp | ! | " | # | $ | % | & | ' |
| 4 | ( | ) | * | + | , | - | . | / | 0 | 1 |
| 5 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | : | ; |
| 6 | < | = | > | ? | @ | A | B | C | D | E |
| 7 | F | G | H | I | J | K | L | M | N | O |
| 8 | P | Q | R | S | T | U | V | W | X | Y |
| 9 | Z | [ | \ | ] | ^ | _ | ` | a | b | c |
| 10 | d | e | f | g | h | i | j | k | l | m |
| 11 | n | o | p | q | r | s | t | u | v | w |
| 12 | x | y | z | { | | | } | ~ | del |  |

Fig. B.1 | ASCII character set.

The digits at the left of the table are the left digits of the decimal equivalents (0–127) of the character codes, and the digits at the top of the table are the right digits of the character codes. For example, the character code for "F" is 70, and the character code for "&" is 38.

Most users of this book are interested in the ASCII character set used to represent English characters on many computers. The ASCII character set is a subset of the Unicode character set used by Java to represent characters from most of the world's languages. For more information on the Unicode character set, see the web bonus Appendix N.

## Keywords and Reserved Words

| Java Keywords |
|---|---|
| abstract | assert | boolean | break | byte |
| case | catch | char | class | continue |
| default | do | double | else | enum |
| extends | final | finally | float | for |
| if | implements | import | instanceof | int |
| interface | long | native | new | package |
| private | protected | public | return | short |
| static | strictfp | super | switch | synchronized |
| this | throw | throws | transient | try |
| void | volatile | while |  |  |
| *Keywords that are not currently used* |
| const | goto |  |  |  |

Fig. C.1 | Java keywords.

Java also contains the reserved words true and false, which are boolean literals, and null, which is the literal that represents a reference to nothing. Like keywords, these reserved words cannot be used as identifiers.

## Primitive Types

| Type | Size in bits | Values | Standard |
|---|---|---|---|
| boolean |  | true or false
[Note: A boolean's representation is specific to the Java Virtual Machine on each platform.] |  |
| char | 16 | '\u0000' to '\uFFFF' (0 to 65535) | (ISO Unicode character set) |
| byte | 8 | -128 to +127 (-2^7 to 2^7 - 1) |  |
| short | 16 | -32,768 to +32,767 (-2^15 to 2^15 - 1) |  |
| int | 32 | -2,147,483,648 to +2,147,483,647 (-2^31 to 2^31 - 1) |  |
| long | 64 | -9,223,372,036,854,775,808 to +9,223,372,036,854,775,807 (-2^63 to 2^63 - 1) |  |
| float | 32 | Negative range:
-3.4028234663852886E+38 to
-1.4012984643248170e-45
Positive range:
1.4012984643248170e-45 to
3.4028234663852886E+38 | (IEEE 754 floating point) |
| double | 64 | Negative range:
-1.7976931348623157E+308 to
-4.94065645841246544e-324
Positive range:
4.94065645841246544e-324 to
1.7976931348623157E+308 | (IEEE 754 floating point) |

Fig. D.1 | Java primitive types.

For more information on IEEE 754 visit grouper.ieee.org/groups/754/. For more information on Unicode, see Appendix N.

## Using the Java API Documentation

### E.1 Introduction

The Java class library contains thousands of predefined classes and interfaces that programmers can use to write their own applications. These classes are grouped into packages based on their functionality. For example, the classes and interfaces used for file processing are grouped into the java.io package, and the classes and interfaces for networking applications are grouped into the java.net package. The Java API documentation lists the public and protected members of each class and the public members of each interface in the Java class library. The documentation overviews all the classes and interfaces, summarizes their members (i.e., the fields, constructors and methods of classes, and the fields and methods of interfaces) and provides detailed descriptions of each member. Most Java programmers rely on this documentation when writing programs. Normally, programmers would search the API to find the following:

- 1. The package that contains a particular class or interface.
- 2. Relationships between a particular class or interface and other classes and interfaces.
- 3. Class or interface constants—normally declared as public static final fields.
- 4. Constructors to determine how an object of the class can be initialized.
- 5. The methods of a class to determine whether they’re static or non-static, the number and types of the arguments you need to pass, the return types and any exceptions that might be thrown from the method.

In addition, programmers often rely on the documentation to discover classes and interfaces that they have not used before. For this reason, we demonstrate the documentation with classes you know and classes you may not have studied yet. We show how to use the documentation to locate the information you need to use a class or interface effectively.

### E.2 Navigating the Java API

The Java API documentation can be downloaded to your local hard disk or viewed online. To download the Java API documentation, go to www.oracle.com/technetwork/java/javase/downloads/index.html/ scroll down to the Additional Resources section and click the Download Zip button to the right of Java SE 6 Documentation. You’ll be asked to accept a license agreement. To do this, click Accept, then click Continue. Click the link to

the ZIP file to begin downloading it. After downloading the file, you can use a program such as WinZip (www.winzip.com) to extract the files. If you’re using Windows, extract the contents to your JDK’s installation directory. To view the API documentation on your local hard disk in Microsoft Windows, open C:\Program Files\Java\YourJDKVersion\docs\api\index.html page in your browser. To view the API documentation online, go to download.oracle.com/javase/6/docs/api/ (Fig. E.1).

![](img/009e962758dcc71dbc43a493362e6dc0_1408_0.png)

Fig. E.1 | Java API overview. (Courtesy of Oracle Corporation)

# Frames in the API Documentation’s index.html Page

The API documentation is divided into three frames (see Fig. E.1). The upper-left frame lists all of the Java API’s packages in alphabetical order. The lower-left frame initially lists the Java API’s classes and interfaces in alphabetical order. Interface names are displayed in italic. When you click a specific package in the upper-left frame, the lower-left frame lists the classes and interfaces of the selected package. The right frame initially provides a brief description of each package of the Java API specification—read this overview to become familiar wth the general capabilities of the Java APIs. If you select a class or interface in the lower-left frame, the right frame displays information about that class or interface.

# Important Links in the index.html Page

At the top of the right frame (Fig. E.1), there are four links—Tree, Deprecated, Index and Help. The Tree link displays the hierarchy of all packages, classes and interfaces in a tree structure. The Deprecated link displays interfaces, classes, exceptions, fields, constructors and methods that should no longer be used. The Index link displays classes, interfaces,
