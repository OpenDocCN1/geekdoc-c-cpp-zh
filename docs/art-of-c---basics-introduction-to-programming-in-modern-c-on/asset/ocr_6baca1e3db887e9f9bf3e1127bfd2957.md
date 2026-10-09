```
// If the first operand is null, then it returns the second
// argument as the value of the expression.
// In this particular case, the second argument of the first
// null-coalescing operator is
//    another null-coalescing operator, whose second argument is
//    to throw an exception.
// In the modern C#, the throw clause is an expression, not a
//    statement.

// The assignment to the discard variable (_) is used to make the
//    whole expression a statement.
//    Otherwise, it will be syntactically invalid.

// BTW, the assignment is also an expression in the modern C#.
// Both the throw and the assignment expressions can be used as
//    statements by themselves.
// Just add the semicolon at the end. ;}

return op.Char switch {
'+' => lhs! + rhs!,
'-' => lhs! - rhs!,
'*' => lhs! * rhs!,
'/' => lhs! / rhs!,
_ => null,
};

}

private static Token ParseWord(string word) {
Token tok = Token.InvalidToken;
if (long.TryParse(word, out long l)) {
tok = new IntToken(l);
} else if (double.TryParse(word, out double d)) {
tok = new FloatToken(d);
} else if (char.TryParse(word, out char c) &&
OperatorToken.IsValid(c)) {
tok = new OperatorToken(c);
}
return tok;
}
```