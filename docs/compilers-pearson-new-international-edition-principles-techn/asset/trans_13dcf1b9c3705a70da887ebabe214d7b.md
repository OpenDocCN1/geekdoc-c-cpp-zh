

## 附录A. 一个完整的前端

### A.8. 语法分析器

```java
3) public class Parser {
4)     private Lexer lex;        // lexical analyzer for this parser
5)     private Token look;       // lookahead token
6)     Env top = null;           // current or top of symbol table
7)     int used = 0;             // storage used for declarations
8)     public Parser(Lexer l) throws IOException { lex = l; move(); }
9)     void move() throws IOException { look = lex.scan(); }
10)    void error(String s) { throw new Error("near line "+lex.line+": "+s); }
11)    void match(int t) throws IOException {
12)        if( look.tag == t ) move();
13)        else error("syntax error");
14)    }
```

与第2.5节中的简单表达式翻译器类似，类`Parser`为每个非终结符提供了一个过程。这些过程基于通过消除第A.1节中源语言文法中的左递归而得到的文法。

语法分析从调用`program`过程开始，该过程调用`block()`（第16行）来解析输入流并构建语法树。第17-18行生成中间代码。

```java
15)    public void program() throws IOException {  // program -> block
16)        Stmt s = block();
17)        int begin = s.newLabel();  int after = s.newLabel();
18)        s.emitLabel(begin);  s.gen(begin, after);  s.emitLabel(after);
19)    }
```

符号表的处理在过程`block`中明确展示。³ 变量`top`（在第5行声明）保存顶层符号表；变量`savedEnv`（第21行）是指向前一个符号表的链接。

```java
20)    Stmt block() throws IOException {  // block -> { decls stmts }
21)        match('{');  Env savedEnv = top;  top = new Env(top);
22)        decls(); Stmt s = stmts();
23)        match('}');  top = savedEnv;
24)        return s;
25)    }
```

声明会为标识符生成符号表条目（参见第30行）。虽然此处未显示，声明还可能生成在运行时为这些标识符预留存储空间的指令。

```java
26)    void decls() throws IOException {
27)        while( look.tag == Tag.BASIC ) {  // D -> Type ID ;
28)            Type p = type(); Token tok = look; match(Tag.ID); match(';');
29)            Id id = new Id((Word)tok, p, used);
30)            top.put(tok, id);
31)            used = used + p.width;
32)        }
33)    }
34)
35)    Type type() throws IOException {
36)        Type p = (Type)look;              // expect look.tag == Tag.BASIC
36)      match(Tag.BASIC);
37)      if (look.tag != '[') return p; // T -> basic
38)      else return dims(p);             // return array type
39)    }
40)    Type dims(Type p) throws IOException {
41)      match('['); Token t = look; match(Tag.NUM); match(']');
42)      if (look.tag == '[')
43)        p = dims(p);
44)      return new Array(((Num)t).value, p);
45)    }
```

³ 一个更好的替代方案是向类`Env`添加`push`和`pop`方法，当前表可通过静态变量`Env.top`访问。

`stmt`过程包含一个`switch`语句，其各个`case`分支对应于非终结符`Stmt`的产生式。每个分支使用第A.7节中讨论的构造函数为一种结构构建节点。当语法分析器看到`while`和`do`语句的开头关键字时，就会构造相应的节点。这些节点在语句被解析之前构造，以便任何包含在内的`break`语句都可以指向其所在的外层循环。嵌套循环通过使用类`Stmt`中的变量`Stmt.Enclosing`和`savedStmt`（在第52行声明）来维护当前的外层循环。

```java
46)    Stmt stmts() throws IOException {
47)      if (look.tag == '}') return Stmt.Null;
48)      else return new Seq(stmt(), stmts());
49)    }
50)    Stmt stmt() throws IOException {
51)      Expr x; Stmt s, s1, s2;
52)      Stmt savedStmt;        // save enclosing loop for breaks
53)      switch(look.tag) {
54)      case ';':
55)        move();
56)        return Stmt.Null;
57)      case Tag.IF:
58)        match(Tag.IF); match('('); x = bool(); match(')');
59)        s1 = stmt();
60)        if(look.tag != Tag.ELSE) return new If(x, s1);
61)        match(Tag.ELSE);
62)        s2 = stmt();
63)        return new Else(x, s1, s2);
64)      case Tag.WHILE:
65)        While whilenode = new While();
66)        savedStmt = Stmt.Enclosing; Stmt.Enclosing = whilenode;
67)        match(Tag.WHILE); match('('); x = bool(); match(')');
68)        s1 = stmt();
69)        whilenode.init(x, s1);
70)        Stmt.Enclosing = savedStmt;  // reset Stmt.Enclosing
71)        return whilenode;
72)      case Tag.DO:
73)        Do donode = new Do();
74)        savedStmt = Stmt.Enclosing; Stmt.Enclosing = donode;
75)        match(Tag.DO);
76)        s1 = stmt();
77)        match(Tag.WHILE); match('('); x = bool(); match(')'); match(';');
78)        donode.init(s1, x);
79)        Stmt.Enclosing = savedStmt;  // reset Stmt.Enclosing
80)        return donode;
81)       case Tag.BREAK:
82)         match(Tag.BREAK); match(';');
83)         return new Break();
84)       case '{':
85)         return block();
86)       default:
87)         return assign();
88)     }
89)   }
```

为方便起见，赋值语句的代码出现在辅助过程`assign`中。

```java
90)   Stmt assign() throws IOException {
91)     Stmt stmt; Token t = look;
92)     match(Tag.ID);
93)     Id id = top.get(t);
94)     if (id == null) error(t.toString() + " is undeclared");
95)     if (look.tag == '=') {          // S -> id = E ;
96)       move(); stmt = new Set(id, bool());
97)     }
98)     else {                         // S -> L = E ;
99)       Access x = offset(id);
100)      match('='); stmt = new SetElem(x, bool());
101)    }
102)    match(';');
103)    return stmt;
104)  }
```

算术表达式和布尔表达式的解析类似。在每种情况下，都会创建相应的语法树节点。两者的代码生成不同，如第A.5节至第A.6节所讨论。

```java
105)  Expr bool() throws IOException {
106)    Expr x = join();
107)    while( look.tag == Tag.OR ) {
108)      Token tok = look; move(); x = new Or(tok, x, join());
109)    }
110)    return x;
111)  }
112)  Expr join() throws IOException {
113)    Expr x = equality();
114)    while( look.tag == Tag.AND ) {
115)      Token tok = look; move(); x = new And(tok, x, equality());
116)    }
117)    return x;
118)  }
119)  Expr equality() throws IOException {
120)    Expr x = rel();
121)    while( look.tag == Tag.EQ || look.tag == Tag.NE ) {
122)      Token tok = look; move(); x = new Rel(tok, x, rel());
123)    }
124)    return x;
125)  }
126)  Expr rel() throws IOException {
127)    Expr x = expr();
128)     switch( look.tag ) {
129)     case '<': case Tag.LE: case Tag.GE: case '>':
130)         Token tok = look; move(); return new Rel(tok, x, expr());
131)     default:
132)         return x;
133)     }
134) }
135) Expr expr() throws IOException {
136)     Expr x = term();
137)     while( look.tag == '+' || look.tag == '-' ) {
138)         Token tok = look; move(); x = new Arith(tok, x, term());
139)     }
140)     return x;
141) }
142) Expr term() throws IOException {
143)     Expr x = unary();
144)     while(look.tag == '*' || look.tag == '/' ) {
145)         Token tok = look; move(); x = new Arith(tok, x, unary());
146)     }
147)     return x;
148) }
149) Expr unary() throws IOException {
150)     if( look.tag == '-' ) {
151)         move(); return new Unary(Word.minus, unary());
152)     }
153)     else if( look.tag == '!' ) {
154)         Token tok = look; move(); return new Not(tok, unary());
155)     }
156)     else return factor();
157) }
```

语法分析器中其余代码处理表达式中的“因子”。辅助过程`offset`生成数组地址计算的代码，如第6.4.3节所讨论。

```java
158) Expr factor() throws IOException {
159)     Expr x = null;
160)     switch( look.tag ) {
161)     case '(':
162)         move(); x = bool(); match(')');
163)         return x;
164)     case Tag.NUM:
165)         x = new Constant(look, Type.Int);       move(); return x;
166)     case Tag.REAL:
167)         x = new Constant(look, Type.Float);     move(); return x;
168)     case Tag.TRUE:
169)         x = Constant.True;
170)         move(); return x;
171)     case Tag.FALSE:
172)         x = Constant.False;
173)         move(); return x;
174)     default:
175)         error("syntax error");
176)         return x;
177)     case Tag.ID:
178)         String s = look.toString();
179)         Id id = top.get(look);
180)         if (id == null) error(look.toString() + " undeclared");
```

