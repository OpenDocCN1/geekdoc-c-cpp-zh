
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

Each production in the original grammar becomes a method that returns a Parser, a class found inside scala.util.parsing.combinator.Parsers. Currently this is a Parser[Any] to be completely general. Consecutive symbols in the original grammar are joined using the operator. The curly braces are replaced with a call to rep. Had there been square brackets, they would have been replaced with a call to opt. There is also a method called repsep that can be used for alternating productions. This includes things like comma-separated lists.

Using these rules, you can take any CF grammar that you might be interested in using and build a parser for it with little effort. You can use any of these parsers by calling the parseAll method that FormulaP gets via JavaTokenParsers in this example.⁵ The following main will do just that and print the value output produced by the parser.

```
def main(args:Array[String]) {
  println(parseAll(form,"3+5*2").get)
}
```

## 30.3.1 Default Output

If you run that main method you get the following output.

```
(3~List()~List((+~(5~List((*~2)))))
```

The string parses, but the default output is a bit challenging to understand. To do so, we need to know what the default output of different parser elements are.

- String or regular expression - Gives back the String that was matched.
- P ~ Q - Gives back ~(p,q), where p is the match for P and q is the match for Q. Note that ~(p,q) prints out as p~q.
- rep(P) - Give back lists of the matches: List(p1,p2,p3,. . .
- repsep(P,Q) - Give back lists of the matches: List(p1,p2,p3,. . . . Note that while Q can be a full parser, the output is ignored. This is why it is best used for things like comma-separated lists where you do not care about the separators.
- opt(P) - Gives back an Option on the match. If that optional part was not used you get None. Otherwise you get Some(p)

Using this information and the original grammar, you can figure out how this parser produced the output that it did.

## 30.3.2 Specified Output

While the default output provides the full information from the parse, and you could run through it using match statements to extract the desired information, it is often more useful to specify your own output from the parser. This is done using the ^^ method. The signature of ^^ in Parser [+T] is def ^^[U](f: (T) => U): Parser[U]. So it takes a function that converts from the normal output of this parser to some other type, U and gives back a Parser[U].

We can utilize this in the parser we wrote above to make it so that it outputs a numeric solution instead of the default parse output we had above. The first step in doing this is to change the return types of the various productions to Parser[Double]. That will introduce errors that we can fix by introducing the appropriate transformations. The resulting code looks like this.

```
object FormulaP extends JavaTokenParsers {
    def form:Parser[Double] = term ~ rep(("+" | "-") ~ term) ^^ {
        case d ~ lst => lst.foldLeft(d)((n,t) => if(t._1=="+") n+t._2 else n-t._2)
    }
    def term:Parser[Double] = factor ~ rep(("*" | "/") ~ factor) ^^ {
        case d ~ lst => lst.foldLeft(d)((n,t) => if(t._1=="*") n*t._2 else n/t._2)
    }
    def factor:Parser[Double] = floatingPointNumber ^^ (_.toDouble) | ("(" ~> form <~ ")")

    def main(args:Array[String]) {
        println(parseAll(form,"3+5*2").get)
    }
}
```

The simplest application of ^^ in this example is after floatingPointNumber. That is a Parser[String] so the normal output is just a String that we can convert to a Double with a call to toDouble. The other two productions follow the ^^ with partial functions that get converted to full functions for us. Each of these has a case that match a number followed by a tilde and a list. The number will be the result of the first term or factor. The list will be the result of rep, which is a List[[String,Double]]. To get an answer, we need to run through the list accumulating a value. At each step, the proper operation should be applied to the current value and the parse of what follows the operator. This can be done in short form using foldLeft. Note that the ~ type works with infix pattern matching and has _1 and _2 methods like a tuple for getting to the first and second elements.

The parser for factor throws in something else to keep this code compact. It uses operators where a < or > is put before or after the ~. These operators give you a shorthand way of ignoring parts of the match in the output. The direction the arrow points is toward the thing you actually care about. Without these, we would have had to follow that last case with a ^^ operator and a function that pulls off the parentheses and discards them.

With these changes, you can run this program and see that now the output is 13.0. Compare this to our original recursive parser that worked with these same operations and you will find that this is significantly shorter. However, this version is also completely opaque to anyone who is not familiar with CF grammars or combinator parsers.

There are, of course, many other options and possibilities with combinator parsers. Looking through the API at classes such as scala.util.parsing.combinator.Parsers and scala.util.parsing.combinator.Parsers.Parser can give you a quick view of some of the possibilities.

## 30.4 Project Integration

Now it is time to put everything together, including some concepts from the last chapter. The FormulaP class can be expanded to parse to a tree instead of a Double. This will allow the use of variables with good speed. To show the true power of the combinator parsers, this implementation will include not only the four basic math operations and a few extra functions, it will also include exponentiation and an if conditional. These two features present interesting challenges. Exponentiation is left associative while the other operators are right associative. In order to have an if, we have to have comparison operators that give back Booleans. It would also be nice to have the standard Boolean operators as well. All of this needs to be integrated into a system that preserves proper order of operation.

To start off, we need to develop a CF grammar that will parse this little language that we are trying to implement. Here is the one we will use in the code.⁶

```
cond ::= "if(" bform ")" cond "else" cond | form
form ::= term {(" + " | " - ") term}
term ::= exp {(" * " | " / ") exp}
exp ::= func {" ^" func}
func ::= "sin" | "cos" | "tan" | "sqrt" "(" cond ")" | factor
factor ::= floatingPointNumber | "(" form ")"
bform ::= bterm {"||" bterm}
```

⁶This grammar includes some of those elements that go beyond the scope of this book. For example, if you change the first production to cond ::= form | "if(" bform ")" cond "else" cond it runs into problems because the string "if" is a valid identifier which matches form.
