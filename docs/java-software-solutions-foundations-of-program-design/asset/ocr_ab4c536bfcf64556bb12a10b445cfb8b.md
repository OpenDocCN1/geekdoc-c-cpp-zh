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