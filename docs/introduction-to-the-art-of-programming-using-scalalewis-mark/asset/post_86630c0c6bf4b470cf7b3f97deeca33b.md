
## 30.1.3 Context-Sensitive Grammars

The next step up the hierarchy removes the limitation that choice of production can not depend on what is around the non-terminal. The general form of the rule is αAβ → αγβ, where α, β, and γ are all arbitrary strings of terminals and non-terminals and are potentially empty. Note that the α and β are not really involved in the production. Instead, they simply limit when the production can be applied.

Context-sensitive grammars are significantly harder to work with than context-free grammars and the number of applications that require context-sensitivity is fairly limited. For that reason, we will not go into any detail on their usage.

## 30.1.4 Recursively Enumerable Grammars

The most powerful class of grammars in the Chomsky hierarchy is the set of recursively enumerable grammars. There are no restrictions on the productions of these grammars. You can have anything on the left-hand side produce whatever you want on the right-hand side. The truly remarkable thing about this class of grammars is that it is a full model of computation. Anything that is computable, in the theoretical sense of the Turing machine or the lambda calculus, can be computed with a properly designed recursively enumerable grammar.

This brief introduction to Chomsky grammars and the Chomsky hierarchy serves as a foundation for the rest of this chapter. However, it is a much broader topic and interested readers should do a bit more exploration of the topic. If nothing else, a proper course on the theory of Computer Science should cover these topics in significantly greater detail than has been presented here.

## 30.2 Regular Expressions

The theoretical underpinnings of Computer Science are extremely important for a variety of reasons, and they play a significant role in major developments in the field. However, the primary focus of this book is on the development of problem solving and programming skills. For that reason, we now turn our focus to the more practical applications of grammars and languages, beginning with regular expressions.

As the name implies, regular expressions are related to regular grammars. They provide a simple mechanism for matching and parsing text. As with regular grammars, they have their limitations. They are still quite powerful and for the problems they are good at, they can make life a whole lot easier.

Regular expressions are typically written as strings with a particular format where certain characters have special meaning. They are used by quite a few different tools, including some that you have been using for a while now. Both grep and the search feature of vi make use of regular expressions. Their tight integration into the programming language Perl was a significant part of why many people used that language for small text processing tasks. Even the split method we have been using on strings uses regular expressions.

While most of the aspects of regular expressions are fairly uniform, there are some features that differ from one implementation to another. Regular expressions in Scala are supported by the scala.util.matching.Regex class and companion object and they are built on top of the Java implementation in java.util.regex. The following subsections will go through a number of the major features of regular expressions. For a more definitive

example regular expression also illustrates that because parentheses are special characters used for grouping in regular expressions, they have to be escaped if you want to match one.

### 30.2.3 Greedy Quantifiers

The real power of regular expressions comes in with quantifiers. Quantifiers allow you to have some control over the number of times an expression will occur. The default quantifiers are called “greedy” quantifiers because they will match as many characters as possible while still allowing the whole pattern to be matched. There are six options for the greedy quantifiers.

- X? - Matches the pattern X or nothing. Think of this as being 0 or 1 times.
- X* - Matches nothing or the pattern X repeated any number of times. Think of this as 0 or more times.
- X+ - Matches the pattern X 1 or more times.
- X{n} - Matches the pattern X repeated exactly n times.
- X{n,} - Matches the pattern X repeated n or more times.
- X{n,m} - Matches the pattern X repeated at least n times, but not more than m times.

The regular expression for the phone number could have been expressed with quantifiers as \((\d{3})\) ((\d{3})-(\d{4})). These quantifiers also allow us to express the languages for the grammars described in subsection 30.1.1. For example a+b+ matches one or more “a”s followed by one or more “b”s. Note that there is not a good way, using these quantifiers, to allow the number of characters of each type to match without specifying how many times they occur.

This should now make it clear why the argument passed to split when we wanted to break a string on spaces was " +". The + here is a quantifier so that this matches one or more spaces. Just in case the user also used tabs, it might be safer to use "\s+".

There are also options for quantifiers that are not greedy. The interested reader is directed to the Java API and other sources for information on reluctant and possessive quantifiers.

### 30.2.4 Boundary Requirements

The last option of regular expressions that we will consider here is boundary requirements. In the general usage, regular expressions can be used to match any part of a string and can be used to do multiple matches inside of a single string. There are situations where you want to restrict the generality of the matches. For this you can put characters at the beginning of the end of the regular expression to specify where it needs to begin or end. The following as some of the allowed options.

- ^ - As the first character in a regular expressions it requires the match to start at the beginning of a line.
- $ - As the last character in a regular expression it requires the match to end at the end of a line.
- \b - Can be placed at the beginning or end of a regular expression forcing the match to start or end on a word boundary.

refer to the variable declared above the method. We want to do this using a variable with a name that starts with a lowercase letter, we have to use backticks in the pattern like this.

```
val `commandSplit`(command,_,rest) = input
```

The choice to make variables used in patterns start with capital letters is simply one of style. You can decide which style you prefer.

The place where regular expression patterns are probably most useful is in for loops. Recall that what you type before <- in a for loop is matched as a val pattern. Anything that does not match is skipped. This is remarkably helpful for regular expressions if you are running through a collection of strings where some might not match what you are looking for.

To see this, consider having a file where some of the lines are numbered and others are not. You only care about the ones that are numbered and they all have, for the first non-space characters, digits followed by a period. After the period is text you care about. You want to built a Map[Int,String] that lets you quickly look up a string based on the number of its line. The following code will do this for you.

```
val NumberedLine = """\s*(\d+)\.(.+ )""".r
val source = Source.fromFile(fileName)
val lines = source.getLines
val numberedLines = (for(NumberedList(num,text) <- lines) yield {
    num -> text
}).toMap
source.close
```

The for loop will only execute on lines matching the pattern and skip anything that does not match. This produces compact and fairly easy to maintain code.

### 30.2.6 Drawback of Regular Expressions

The primary drawback of regular expressions is that they can be cryptic and somewhat difficult to maintain. Indeed, languages that highlight the use of regular expressions are often derided for their lack of readability. Coming up with exactly the right regular expression for a problem can also be quite challenging. This is expressed in this oft-repeated quote.

> Some people, when confronted with a problem, think
> "I know, I'll use regular expressions." Now they have two problems.
> - Jamie Zawinski (1997 Usenet post)

There is inevitably some truth to this quote. However, hopefully the examples above have shown you that in situations where regular expressions work well, they can make life much easier. Just do not try to use them to solve every problem you encounter.

## 30.3 Context-Free Parsers

What options do you have if you need to parse text that is beyond the power of regular expressions? Scala includes the package scala.util.parsing which has a number of different subpackages that provide different parsing capabilities. We will focus on the
