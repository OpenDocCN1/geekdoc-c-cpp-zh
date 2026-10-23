scala.util.parsing.combinator package which gives us the ability to parse context-free grammars.⁴

The introduction to context-free, CF, grammars given in subsection 30.1.2 used a notation fitting with theoretical Computer Science. Like mathematicians, theoretical computer scientists are quite happy to name things using single letters or symbols. In practical application, it is typically helpful to use longer, more informative names. The symbology is also altered a bit when expressing CF grammars for things like programming languages. To illustrate this, we will go back to the example of formula parsing that we have utilized in the last two chapters. The CF grammar for a basic mathematical expression using only the four primary operators can be written this way.

```
form ::= term {(" +" | " -") term}
term ::= factor {(" *" | " /") factor}
factor ::= floatingPointNumber | "(" form ")"
```

In this notation, the curly braces indicate elements that can be repeated zero or more times. It is also possible to use square brackets to indicate things that are optional.

This grammar says that a formula is a term followed by zero or more + or − signs followed by terms. The term is a factor followed by factors with * or / between them. Lastly, the factor can be a number or a full formula in parentheses. Play with this to convince yourself that it can represent the full range of possibilities that are desired. It is also worth noting that this grammar does proper order of operations and * and / are bound a level below the + and −.

Using the combinator parser library, this converts fairly directly to the following Scala code.

```
object FormulaP extends JavaTokenParsers {
  def form:Parser[Any] = term ~ rep(("+") | "-") ~ term
  def term:Parser[Any] = factor ~ rep(("*") | "/") ~ factor
  def factor:Parser[Any] = floatingPointNumber | "(" ~ form ~ ")"
}
```

Each production in the original grammar becomes a method that returns a Parser, a class found insider scala.util.parser.combinator.Parsers. Currently this is a Parser[Any] to be completely general. Consecutive symbols in the original grammar are joined using the operator. The curly braces are replaced with a call to rep. Had there been square brackets, they would have been replaced with a call to opt. There is also a method called repsep that can be used for alternating productions. This includes things like comma-separated lists.

Using these rules, you can take any CF grammar that you might be interested in using and build a parser for it with little effort. You can use any of these parsers by calling the parseAll method that FormulaP gets via JavaTokenParsers in this example.⁵ The following main will do just that and print the value output produced by the parser.

```
def main(args:Array[String]) {
  println(parseAll(form,"3+5*2").get)
}
```