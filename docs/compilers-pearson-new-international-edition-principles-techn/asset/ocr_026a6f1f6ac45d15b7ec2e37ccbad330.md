```
```text
8)     eq    = new Word( "==", Tag.EQ  ),  ne = new Word( "!=", Tag.NE ),
9)     le    = new Word( "<=", Tag.LE  ),  ge = new Word( ">=", Tag.GE ),
10)    minus = new Word( "minus", Tag.MINUS ),
11)    True  = new Word( "true", Tag.TRUE ),
12)    False = new Word( "false", Tag.FALSE ),
13)    temp  = new Word( "t", Tag.TEMP );
14) }
```
```

Class Real is for floating point numbers:

```
```java
1) package lexer;                         // File Real.java
2) public class Real extends Token {
3)     public final float value;
4)     public Real(float v) { super(Tag.REAL); value = v; }
5)     public String toString() { return "" + value; }
6) }
```
```

The main method in class Lexer, function scan, recognizes numbers, identifiers, and reserved words, as discussed in Section 2.6.5.

Lines 9-13 in class Lexer reserve selected keywords. Lines 14-16 reserve lexemes for objects defined elsewhere. Objects Word.True and Word.False are defined in class Word. Objects for the basic types int, char, bool, and float are defined in class Type, a subclass of Word. Class Type is from package symbols.

```
```java
1) package lexer;                         // File Lexer.java
2) import java.io.*; import java.util.*; import symbols.*;
3) public class Lexer {
4)     public static int line = 1;
5)     char peek = ' ';
6)     Hashtable words = new Hashtable();
7)     void reserve(Word w) { words.put(w.lexeme, w); }
8)     public Lexer() {
9)         reserve( new Word("if",     Tag.IF)   );
10)        reserve( new Word("else",   Tag.ELSE) );
11)        reserve( new Word("while",  Tag.WHILE) );
12)        reserve( new Word("do",     Tag.DO)   );
13)        reserve( new Word("break",  Tag.BREAK) );
14)        reserve( Word.True );  reserve( Word.False );
15)        reserve( Type.Int );   reserve( Type.Char );
16)        reserve( Type.Bool );  reserve( Type.Float );
17)    }
```
```

Function readch() (line 18) is used to read the next input character into variable peek. The name readch is reused or overloaded (lines 19-24) to help recognize composite tokens. For example, once input < is seen, the call readch('=') reads the next character into peek and checks whether it is =.

```
```java
18)    void readch() throws IOException { peek = (char)System.in.read(); }
19)    boolean readch(char c) throws IOException {
20)        readch();
21)        if( peek != c ) return false;
22)        peek = ' ';
23)        return true;
24)    }
```
```