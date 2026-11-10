# A.5. INTERMEDIATE CODE FOR EXPRESSIONS

```
```java
7)    Temp t = new Temp(type);
8)    emit(t.toString() + " = " + x.toString() );
9)    return t;
10)   }
11) }
```
```

Class Arith implements binary operators like + and *. Constructor Arith begins by calling super(tok,null) (line 6), where tok is a token representing the operator and null is a placeholder for the type. The type is determined on line 7 by using Type.max, which checks whether the two operands can be coerced to a common numeric type; the code for Type.max is in Section A.4. If they can be coerced, type is set to the result type; otherwise, a type error is reported (line 8). This simple compiler checks types, but it does not insert type conversions.

```
```java
1) package inter;                         // File Arith.java
2) import lexer.*; import symbols.*;
3) public class Arith extends Op {
4)     public Expr expr1, expr2;
5)     public Arith(Token tok, Expr x1, Expr x2) {
6)         super(tok); expr1 = x1; expr2 = x2;
7)         type = Type.max(expr1.type, expr2.type);
8)         if (type == null) error("type error");
9)     }
10)    public Expr gen() {
11)        return new Arith(op, expr1.reduce(), expr2.reduce());
12)    }
13)    public String toString() {
14)        return expr1.toString()+" "+op.toString()+" "+expr2.toString();
15)    }
16) }
```
```

Method gen constructs the right side of a three-address instruction by reducing the subexpressions to addresses and applying the operator to the addresses (line 11, file Arith.java). For example, suppose gen is called at the root for a+b*c. The calls to reduce return a as the address for subexpression a and a temporary t as the address for b*c. Meanwhile, reduce emits the instruction t=b*c. Method gen returns a new Arith node, with operator * and addresses a and t as operands.

It is worth noting that temporary names are typed, along with all other expressions. The constructor Temp is therefore called with a type as a parameter (line 6, file Temp.java).

```
```java
1) package inter;                         // File Temp.java
2) import lexer.*; import symbols.*;
3) public class Temp extends Expr {
```
```

¹For error reporting, field lexline in class Node records the current lexical line number when a node is constructed. We leave it to the reader to track line numbers when new nodes are constructed during intermediate code generation.

²An alternative approach might be for the constructor to take an expression node as a parameter, so it can copy the type and lexical position of the expression node.