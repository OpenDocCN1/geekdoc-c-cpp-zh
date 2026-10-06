# Introduction to Programming and Problem-Solving Using Scala

+   - The operator is logical negation.
- The || && operators are short-circuit operators.

When building large expressions, the order in which operators are applied is significant. This is called precedence. The precedence of operators in Scala depends on the first character in the operator. Table 3.3 gives a full list of precedence in Scala.

Bits can be viewed as Boolean values. Bit-wise arithmetic is operations that work on numeric numbers as collections of bits instead of normal numbers.

+   - | is bit-wise or.
- & is bit-wise and.
- ^ is bit-wise xor.
- ~ is bit-wise negation.

# 3.8.3 Self-Directed Study

Enter the following statements into the REPL and see what they do. Try some variations to make sure you understand what is going on. Note that some lines read values so the REPL will pause until you enter those values. The outcome of other lines will depend on what you enter.

```
scala val a = readInt()
scala val b = readInt()
scala val minimum = if (a<b) else b
scala if (minimum != (a min b)) {
  println("Oops, something went wrong.")
} else {
  println("That's good.")
}
scala true && true
scala true && false
scala false && true
scala false && false
scala true || true
scala true || false
scala false || true
scala false || false
scala !true
scala true ^ true
scala true ^ false
scala false ^ true
scala false ^ false
scala a < b || {println("a=b"); a >= b }
scala a < b && {println("a=b"); a >= b }
scala match {
  case 7 => "That is a lucky number."
  case 13 => "That is an unlucky number."
  case _ => "I'm not certain about that number."
}
scala 13 & 5
scala a.toBinaryString
```