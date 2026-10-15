
The comments in the Lincoln program represent one of two types of comments allowed in Java. The comments in Lincoln take the following form:

```
// This is a comment.
```

This type of comment begins with a double slash (//) and continues to the end of the line. You cannot have any characters between the two slashes. The computer ignores any text after the double slash to the end of the line. A comment can follow code on the same line to document that particular line, as in the following example:

```
System.out.println ("Monthly Report"); // always use this title
```

The second form a Java comment may have is the following:

```
/* This is another comment. */
```

This comment type does not use the end of a line to indicate the end of the comment. Anything between the initiating slash-asterisk (/*) and the terminating asterisk-slash (*/) is part of the comment, including the invisible newline character that represents the end of a line. Therefore, this type of comment can extend over multiple lines. No space can be between the slash and the asterisk.

If there is a second asterisk following the /* at the beginning of a comment, the content of the comment can be used to automatically generate external documentation about your program by using a tool called javadoc. More information about javadoc is given in Appendix I.

The two basic comment types can be used to create various documentation styles, such as:

```
// This is a comment on a single line.

//------------------------------------------------------------
// Some comments such as those above methods or classes
// deserve to be blocked off to focus special attention
// on a particular aspect of your code. Note that each of
// these lines is technically a separate comment.
//------------------------------------------------------------

/*
    This is one comment
    that spans several lines.
*/
```

Programmers often concentrate so much on writing code that they focus too little on documentation. You should develop good commenting practices and follow them habitually. Comments should be well written, often in complete sentences.

They should not belabor the obvious but should provide appropriate insight into the intent of the code. The following examples are not good comments:

```
System.out.println ("hello"); // prints hello
System.out.println ("test"); // change this later
```

The first comment paraphrases the obvious purpose of the line and does not add any value to the statement. It is better to have no comment than a useless one. The second comment is ambiguous. What should be changed later? When is later? Why should it be changed?

> KEY CONCEPT
> Inline documentation should provide insight into your code. It should not be ambiguous or belabor the obvious.

## Identifiers and Reserved Words

The various words used when writing programs are called identifiers. The identifiers in the Lincoln program are class, Lincoln, public, static, void, main, String, args, System, out, and println. These fall into three categories:

- words that we make up when writing a program (Lincoln and args)
- words that another programmer chose (String, System, out, println, and main)
- words that are reserved for special purposes in the language (class, public, static, and void)

While writing the program, we simply chose to name the class Lincoln, but we could have used one of many other possibilities. For example, we could have called it Quote, or Abe, or GoodOne. The identifier args (which is short for arguments) is often used in the way we use it in Lincoln, but we could have used just about any other identifier in its place.

The identifiers String, System, out, and println were chosen by other programmers. These words are not part of the Java language. They are part of the Java standard library of predefined code, a set of classes and methods that someone has already written for us. The authors of that code chose the identifiers in that code—we're just making use of them.

Reserved words are identifiers that have a special meaning in a programming language and can only be used in predefined ways. A reserved word cannot be used for any other purpose, such as naming a class or method. In the Lincoln program, the reserved words used are class, public, static, and void. Throughout the book, we show Java reserved words in blue type. Figure 1.18 lists all of the Java reserved words in alphabetical order. The words marked with an asterisk have been reserved, but currently have no meaning in Java.

An identifier that we make up for use in a program can be composed of any combination of letters, digits, the underscore character (_), and the dollar sign ($), but it cannot begin with a digit. Identifiers may be of any length.

| abstract | default | goto* | package | this |
| assert | do | if | private | throw |
| boolean | double | implements | protected | throws |
| break | else | import | public | transient |
| byte | enum | instanceof | return | true |
| case | extends | int | short | try |
| catch | false | interface | static | void |
| char | final | long | strictfp | volatile |
| class | finally | native | super | while |
| const* | float | new | switch |  |
| continue | for | null | synchronized |  |

### FIGURE 1.18 Java reserved words

Therefore, total, label17, nextStockItem, NUM_BOXES, and $amount are all valid identifiers, but 4th_word and coin#value are not valid.

Both uppercase and lowercase letters can be used in an identifier, and the difference is important. Java is case sensitive, which means that two identifier names that differ only in the case of their letters are considered to be different identifiers. Therefore, total, Total, ToTaL, and TOTAL are all different identifiers. As you can imagine, it is not a good idea to use multiple identifiers that differ only in their case, because they can be easily confused.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_59_0.png)

Although the Java language doesn’t require it, using a consistent case format for each kind of identifier makes your identifiers easier to understand. There are various Java conventions regarding identifiers that should be followed, though technically they don’t have to be. For example, we use title case (uppercase for the first letter of each word) for class names. Throughout the text, we describe the preferred case style for each type of identifier when it is first encountered.

While an identifier can be of any length, you should choose your names carefully. They should be descriptive but not verbose. You should avoid meaningless names such as a or x. An exception to this rule can be made if the short name is actually descriptive, such as using x and y to represent (x, y) coordinates on a two-dimensional grid. Likewise, you should not use unnecessarily long names, such as the identifier theCurrentItemBeingProcessed. The name currentItem would serve just as well. As you might imagine, the use of identifiers that are verbose is a much less prevalent problem than the use of names that are not descriptive.

You should always strive to make your programs as readable as possible. Therefore, you should always be careful when abbreviating words. You might think curStVal is a good name to represent the current stock value, but another person trying to understand the code may have trouble figuring out what you meant. It might not even be clear to you two months after writing it.

KEY CONCEPT
Java is case sensitive. The uppercase and lowercase versions of a letter are distinct.

KEY CONCEPT
Identifier names should be descriptive and readable.

## White Space

All Java programs use white space to separate the words and symbols used in a program. White space consists of blanks, tabs, and newline characters. The phrase “white space” refers to the fact that, on a white sheet of paper with black printing, the space between the words and symbols is white. The way a programmer uses white space is important because it can be used to emphasize parts of the code and can make a program easier to read.

Except when it’s used to separate words, the computer ignores white space. It does not affect the execution of a program. This fact gives programmers a great deal of flexibility in how they format a program. The lines of a program should be divided in logical places, and certain lines should be indented and aligned so that the program’s underlying structure is clear.

Because white space is ignored, we can write a program in many different ways. For example, taking white space to one extreme, we could put as many words as possible on each line. The code in Listing 1.2, the Lincoln2 program, is formatted quite differently from Lincoln but prints the same message.

KEY CONCEPT
Appropriate use of white space makes a program easier to read and understand.
