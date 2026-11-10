
## APPENDIX A. A COMPLETE FRONT END

### A.4 Symbol Tables and Types

Package symbols implements symbol tables and types. Class Env is essentially unchanged from Fig. 2.37. Whereas class Lexer maps strings to words, class Env maps word tokens to objects of class Id, which is defined in package inter along with the classes for expressions and statements.

```java
1) package symbols;                         // File Env.java
2) import java.util.*; import lexer.*; import inter.*;
3) public class Env {
4)     private Hashtable table;
5)     protected Env prev;
6)     public Env(Env n) { table = new Hashtable(); prev = n; }
7)     public void put(Token w, Id i) { table.put(w, i); }
8)     public Id get(Token w) {
9)         for( Env e = this; e != null; e = e.prev ) {
10)            Id found = (Id)(e.table.get(w));
11)            if( found != null ) return found;
12)        }
13)        return null;
14)    }
15) }
```

We define class Type to be a subclass of Word since basic type names like int are simply reserved words, to be mapped from lexemes to appropriate objects by the lexical analyzer. The objects for the basic types are Type.Int, Type.Float, Type.Char, and Type.Bool (lines 7-10). All of them have inherited field tag set to Tag.BASIC, so the parser treats them all alike.

```java
1) package symbols;                         // File Type.java
2) import lexer.*;
3) public class Type extends Word {
4)     public int width = 0;                  // width is used for storage allocation
5)     public Type(String s, int tag, int w) { super(s, tag); width = w; }
6)     public static final Type
7)         Int  = new Type("int",  Tag.BASIC, 4 ),
8)         Float = new Type("float", Tag.BASIC, 8 ),
9)         Char = new Type("char", Tag.BASIC, 1 ),
10)        Bool = new Type("bool", Tag.BASIC, 1 );
```

Functions numeric (lines 11-14) and max (lines 15-20) are useful for type conversions.

```java
11)    public static boolean numeric(Type p) {
12)        if (p == Type.Char || p == Type.Int || p == Type.Float) return true;
13)        else return false;
14)    }
15)    public static Type max(Type p1, Type p2) {
16)        if ( ! numeric(p1) || ! numeric(p2) ) return null;
17)        else if ( p1 == Type.Float || p2 == Type.Float ) return Type.Float;
18)        else if ( p1 == Type.Int   || p2 == Type.Int   ) return Type.Int;
19)        else return Type.Char;
20)    }
21) }
```

Conversions are allowed between the “numeric” types Type.Char, Type.Int, and Type.Float. When an arithmetic operator is applied to two numeric types, the result has the “max” of the two types.

Arrays are the only constructed type in the source language. The call to super on line 7 sets field width, which is essential for address calculations. It also sets lexeme and tok to default values that are not used.

```java
1) package symbols;              // File Array.java
2) import lexer.*;
3) public class Array extends Type {
4)     public Type of;             // array *of* type
5)     public int size = 1;         // number of elements
6)     public Array(int sz, Type p) {
7)         super("[]", Tag.INDEX, sz*p.width); size = sz;  of = p;
8)     }
9)     public String toString() { return "[" + size + "] " + of.toString(); }
10) }
```

### A.5 Intermediate Code for Expressions

Package inter contains the Node class hierarchy. Node has two subclasses: Expr for expression nodes and Stmt for statement nodes. This section introduces Expr and its subclasses. Some of the methods in Expr deal with booleans and jumping code; they will be discussed in Section A.6, along with the remaining subclasses of Expr.

Nodes in the syntax tree are implemented as objects of class Node. For error reporting, field lexline (line 4, file Node.java) saves the source-line number of the construct at this node. Lines 7-10 are used to emit three-address code.

```java
1) package inter;                  // File Node.java
2) import lexer.*;
3) public class Node {
4)     int lexline = 0;
5)     Node() { lexline = Lexer.line; }
6)     void error(String s) { throw new Error("near line "+lexline+": "+s); }
7)     static int labels = 0;
8)     public int newlabel() { return ++labels; }
9)     public void emitlabel(int i) { System.out.print("L" + i + ":"); }
10)    public void emit(String s) { System.out.println("\t" + s); }
11) }
```

Expression constructs are implemented by subclasses of Expr. Class Expr has fields op and type (lines 4-5, file Expr.java), representing the operator and type, respectively, at a node.

```java
1) package inter;                 // File Expr.java
2) import lexer.*; import symbols.*;
3) public class Expr extends Node {
4)     public Token op;
5)     public Type type;
6)     Expr(Token tok, Type p) { op = tok; type = p; }
```

Method `gen` (line 7) returns a “term” that can fit the right side of a three-address instruction. Given expression $E = E_1 + E_2$, method `gen` returns a term $x_1+x_2$, where $x_1$ and $x_2$ are addresses for the values of $E_1$ and $E_2$, respectively. The return value thus is appropriate if this object is an address; subclasses of `Expr` typically reimplement `gen`.

Method `reduce` (line 8) computes or “reduces” an expression down to a single address; that is, it returns a constant, an identifier, or a temporary name. Given expression $E$, method `reduce` returns a temporary $t$ holding the value of $E$. Again, this is an appropriate return value if this object is an address.

We defer discussion of methods `jumping` and `emitjumps` (lines 9-18) until Section A.6; they generate jumping code for boolean expressions.

```java
7)   public Expr gen() { return this; }
8)   public Expr reduce() { return this; }
9)   public void jumping(int t, int f) { emitjumps(toString(), t, f); }
10)  public void emitjumps(String test, int t, int f) {
11)      if( t != 0 && f != 0 ) {
12)          emit("if " + test + " goto L" + t);
13)          emit("goto L" + f);
14)      }
15)      else if( t != 0 ) emit("if " + test + " goto L" + t);
16)      else if( f != 0 ) emit("iffalse " + test + " goto L" + f);
17)      else ; // nothing since both t and f fall through
18)  }
19)  public String toString() { return op.toString(); }
20) }
```

Class `Id` inherits the default implementations of `gen` and `reduce` in class `Expr`, since an identifier is an address.

```java
1) package inter;                         // File Id.java
2) import lexer.*; import symbols.*;
3) public class Id extends Expr {
4)     public int offset;      // relative address
5)     public Id(Word id, Type p, int b) { super(id, p); offset = b; }
6) }
```

The node for an identifier of class `Id` is a leaf. The call `super(id,p)` (line 5, file *Id.java*) saves `id` and `p` in inherited fields `op` and `type`, respectively. Field `offset` (line 4) holds the relative address of this identifier.

Class `Op` provides an implementation of `reduce` (lines 5-10, file *Op.java*) that is inherited by subclasses `Arith` for arithmetic operators, `Unary` for unary operators, and `Access` for array accesses. In each case, `reduce` calls `gen` to generate a term, emits an instruction to assign the term to a new temporary name, and returns the temporary.

```java
1) package inter;                         // File Op.java
2) import lexer.*; import symbols.*;
3) public class Op extends Expr {
4)     public Op(Token tok, Type p) { super(tok, p); }
5)     public Expr reduce() {
6)         Expr x = gen();
```

```java
4)      static int count = 0;
5)      int number = 0;
6)      public Temp(Type p) { super(Word.temp, p); number = ++count; }
7)      public String toString() { return "t" + number; }
8)  }
```

Class Unary is the one-operand counterpart of class Arith:

```java
1) package inter;                             // File Unary.java
2) import lexer.*; import symbols.*;
3) public class Unary extends Op {
4)     public Expr expr;
5)     public Unary(Token tok, Expr x) {    // handles minus, for ! see Not
6)         super(tok, null); expr = x;
7)         type = Type.max(Type.Int, expr.type);
8)         if (type == null ) error("type error");
9)     }
10)    public Expr gen() { return new Unary(op, expr.reduce()); }
11)    public String toString() { return op.toString()+" "+expr.toString(); }
12) }
```

### A.6 Jumping Code for Boolean Expressions

Jumping code for a boolean expression *B* is generated by method jumping, which takes two labels *t* and *f* as parameters, called the true and false exits of *B*, respectively. The code contains a jump to *t* if *B* evaluates to true, and a jump to *f* if *B* evaluates to false. By convention, the special label 0 means that control falls through *B* to the next instruction after the code for *B*.

We begin with class Constant. The constructor Constant on line 4 takes a token tok and a type p as parameters. It constructs a leaf in the syntax tree with label tok and type p. For convenience, the constructor Constant is overloaded (line 5) to create a constant object from an integer.

```java
1) package inter;                           // File Constant.java
2) import lexer.*; import symbols.*;
3) public class Constant extends Expr {
4)     public Constant(Token tok, Type p) { super(tok, p); }
5)     public Constant(int i) { super(new Num(i), Type.Int); }
6)     public static final Constant
7)         True = new Constant(Word.True, Type.Bool),
8)         False = new Constant(Word.False, Type.Bool);
9)     public void jumping(int t, int f) {
10)        if ( this == True && t != 0 ) emit("goto L" + t);
11)        else if ( this == False && f != 0) emit("goto L" + f);
12)    }
13) }
```

Method jumping (lines 9-12, file *Constant.java*) takes two parameters, labels *t* and *f*. If this constant is the static object True (defined on line 7) and *t* is not the special label 0, then a jump to *t* is generated. Otherwise, if this is the object False (defined on line 8) and *f* is nonzero, then a jump to *f* is generated.
