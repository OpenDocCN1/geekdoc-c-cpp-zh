```
<expression> switch {
<pattern1> => <value1>,
<pattern2> => <value2>,
// ....
_ => <defaultvalue>,
}

```

In this notation, switch is the only keyword. In addition, it uses the "fat arrow" (→), comma (,), underscore (_), and a pair of curly braces ({ and }).

Despite the use of the curly braces, it is an expression, not a statement. It cannot be used as a stand-alone statement. In the sample code, the value of the switch expression is used in the expression body. If we had used a block body, then we would have used return to return this value.

The switch expression works as follows: The type, value, and other properties, etc. of <expression> are computed first. Then they are "matched" against a series of patterns in the switch expression. If it matches any of the patterns, by going through the patterns from top to bottom, then the value of the entire expression is the value specified on the right hand side of ⇒ for that matched pattern.

The patterns in the switch expression have to be "exhaustive". That is, the list of the patterns has to cover all possible cases of the <expression>.

The optional _ identifier like a wildcard. It can be used as a "catch-all" case. If none of the explicit patterns matches, then the value of the default case is used.

C#, as of 9.0, supports many kinds of "patterns". It even supports Boolean combinations of all different patterns, using and, or, and not.

In this sample code, we use the type patterns. (Refer to the C# language reference for all the possible pattern types.) The <expression> is an anonymous tuple, (l, r), in which l and r are the arguments of type T passed in to the Subtract<T>() method.