
## 面向对象与面向阶段

采用面向对象方法时，某个构造的所有代码都收集在该构造对应的类中。或者，采用面向阶段方法时，代码按阶段分组，因此类型检查过程会为每个构造有一个分支，代码生成过程也会为每个构造有一个分支，依此类推。

权衡之处在于，面向对象方法使更改或添加构造（例如“for”语句）更容易，而面向阶段方法使更改或添加阶段（例如类型检查）更容易。使用对象时，可以通过编写一个自包含的类来添加新构造，但对某个阶段的更改（例如插入用于强制转换的代码）需要修改所有受影响的类。使用阶段时，新构造可能导致各阶段过程的修改。

```
stmt → loc = bool ;
     | if ( bool ) stmt
     | if ( bool ) stmt else stmt
     | while ( bool ) stmt
     | do stmt while ( bool ) ;
     | break ;
     | block
loc  → loc [ bool ] | id
```

表达式的产生式处理运算符的结合性和优先级。它们为每个优先级层次使用一个非终结符，并使用非终结符 *factor* 表示括号表达式、标识符、数组引用和常量。

```
bool     → bool || join | join
join     → join && equality | equality
equality → equality == rel | equality != rel | rel
rel      → expr < expr | expr <= expr | expr >= expr |
           expr > expr | expr
expr     → expr + term | expr - term | term
term     → term * unary | term / unary | unary
unary    → ! unary | - unary | factor
factor   → ( bool ) | loc | num | real | true | false
```

## A.2 Main

执行从类 Main 中的方法 main 开始。方法 main 创建一个词法分析器和一个语法分析器，然后调用语法分析器中的方法 program：

```java
1) package main;  // File Main.java
2) import java.io.*; import lexer.*; import parser.*;
3) public class Main {
4)     public static void main(String[] args) throws IOException {
5)         Lexer lex = new Lexer();
6)         Parser parse = new Parser(lex);
7)         parse.program();
8)         System.out.write('\n');
9)     }
10) }
```

## A.3 词法分析器

包 lexer 是第 2.6.5 节中词法分析器代码的扩展。类 Tag 为记号定义常量：

```java
1) package lexer;                 // File Tag.java
2) public class Tag {
3)     public final static int
4)         AND = 256, BASIC = 257, BREAK = 258, DO = 259, ELSE = 260,
5)         EQ = 261, FALSE = 262, GE = 263, ID = 264, IF = 265,
6)         INDEX = 266, LE = 267, MINUS = 268, NE = 269, NUM = 270,
7)         OR = 271, REAL = 272, TEMP = 273, TRUE = 274, WHILE = 275;
8) }
```

其中三个常量 INDEX、MINUS 和 TEMP 不是词法记号；它们将用于语法树。

类 Token 和 Num 与第 2.6.5 节中相同，但增加了方法 toString：

```java
1) package lexer;                 // File Token.java
2) public class Token {
3)     public final int tag;
4)     public Token(int t) { tag = t; }
5)     public String toString() {return "" + (char)tag;}
6) }
```

```java
1) package lexer;                 // File Num.java
2) public class Num extends Token {
3)     public final int value;
4)     public Num(int v) { super(Tag.NUM); value = v; }
5)     public String toString() { return "" + value; }
6) }
```

类 Word 管理保留字、标识符以及诸如 && 的复合记号的词素。它还可用于管理中间代码中运算符的书写形式，例如一元减；例如，源文本 -2 的中间形式为 minus 2。

```java
1) package lexer;                 // File Word.java
2) public class Word extends Token {
3)     public String lexeme = "";
4)     public Word(String s, int tag) { super(tag); lexeme = s; }
5)     public String toString() { return lexeme; }
6)     public static final Word
7)         and = new Word("&&", Tag.AND), or = new Word("||", Tag.OR),
8)         eq = new Word("=", Tag.EQ), ne = new Word("!=", Tag.NE),
9)         le = new Word("<=", Tag.LE), ge = new Word(">=", Tag.GE),
10)        minus = new Word("minus", Tag.MINUS),
11)        True = new Word("true", Tag.TRUE),
12)        False = new Word("false", Tag.FALSE),
13)        temp = new Word("t", Tag.TEMP);
14) }
```

类 Real 用于浮点数：

```java
1) package lexer;                         // File Real.java
2) public class Real extends Token {
3)     public final float value;
4)     public Real(float v) { super(Tag.REAL); value = v; }
5)     public String toString() { return "" + value; }
6) }
```

类 Lexer 中的 main 方法（即函数 scan）识别数字、标识符和保留字，如第 2.6.5 节所述。

类 Lexer 中的第 9-13 行保留选定的关键字。第 14-16 行为在别处定义的对象保留词素。对象 Word.True 和 Word.False 在类 Word 中定义。基本类型 int、char、bool 和 float 的对象在类 Type 中定义，Type 是 Word 的子类。类 Type 来自包 symbols。

```java
1) package lexer;                         // File Lexer.java
2) import java.io.*; import java.util.*; import symbols.*;
3) public class Lexer {
4)     public static int line = 1;
5)     char peek = ' ';
6)     Hashtable words = new Hashtable();
7)     void reserve(Word w) { words.put(w.lexeme, w); }
8)     public Lexer() {
9)         reserve(new Word("if", Tag.IF));
10)        reserve(new Word("else", Tag.ELSE));
11)        reserve(new Word("while", Tag.WHILE));
12)        reserve(new Word("do", Tag.DO));
13)        reserve(new Word("break", Tag.BREAK));
14)        reserve(Word.True);  reserve(Word.False);
15)        reserve(Type.Int);   reserve(Type.Char);
16)        reserve(Type.Bool);  reserve(Type.Float);
17)    }
```

函数 readch()（第 18 行）用于将下一个输入字符读入变量 peek。名称 readch 被重用或重载（第 19-24 行），以帮助识别复合记号。例如，一旦看到输入 <，调用 readch('=') 会将下一个字符读入 peek，并检查它是否为 =。

```java
18) void readch() throws IOException { peek = (char)System.in.read(); }
19) boolean readch(char c) throws IOException {
20)     readch();
21)     if( peek != c ) return false;
22)     peek = ' ';
23)     return true;
24) }
```

函数 scan 首先跳过空白（第 26-30 行）。它在收集单词（第 59-70 行）之前，识别诸如 <= 的复合记号（第 31-44 行）以及诸如 365 和 3.14 的数字（第 45-58 行）。

```java
25)    public Token scan() throws IOException {
26)        for( ; readch() ) {
27)            if( peek == ' ' || peek == '\t' ) continue;
28)            else if( peek == '\n' ) line = line + 1;
29)            else break;
30)        }
31)        switch( peek ) {
32)        case '&':
33)            if( readch('&') ) return Word.and;  else return new Token('&');
34)        case '|':
35)            if( readch('|') ) return Word.or;   else return new Token('|');
36)        case '=':
37)            if( readch('=') ) return Word.eq;   else return new Token('=');
38)        case '!':
39)            if( readch('=') ) return Word.ne;   else return new Token('!');
40)        case '<':
41)            if( readch('=') ) return Word.le;   else return new Token('<');
42)        case '>':
43)            if( readch('=') ) return Word.ge;   else return new Token('>');
44)        }
45)        if( Character.isDigit(peek) ) {
46)            int v = 0;
47)            do {
48)                v = 10*v + Character.digit(peek, 10); readch();
49)            } while( Character.isDigit(peek) );
50)            if( peek != '.' ) return new Num(v);
51)            float x = v; float d = 10;
52)            for(;;) {
53)                readch();
54)                if( ! Character.isDigit(peek) ) break;
55)                x = x + Character.digit(peek, 10) / d; d = d*10;
56)            }
57)            return new Real(x);
58)        }
59)        if( Character.isLetter(peek) ) {
60)            StringBuffer b = new StringBuffer();
61)            do {
62)                b.append(peek); readch();
63)            } while( Character.isLetterOrDigit(peek) );
64)            String s = b.toString();
65)            Word w = (Word)words.get(s);
66)            if( w != null ) return w;
67)            w = new Word(s, Tag.ID);
68)            words.put(s, w);
69)            return w;
70)        }
```

最后，任何剩余字符都作为记号返回（第 71-72 行）。

```java
71)    Token tok = new Token(peek); peek = ' ';
72)    return tok;
73) }
74) }
```

