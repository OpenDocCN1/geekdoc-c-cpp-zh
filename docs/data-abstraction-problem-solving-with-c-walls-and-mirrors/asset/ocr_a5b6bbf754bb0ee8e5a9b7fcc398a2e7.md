# 192 CHAPTER 5 Recursion as a Problem-Solving Technique

7. Implement the algorithm described in this chapter to convert a prefix expression to postfix form.

8. The following is a grammar that allows you to omit parentheses in infix expressions where the precedence rules remove ambiguity. For example, a * b * c means a * (b * c). However, the grammar requires parentheses when would otherwise result. That is, the grammar does not permit left-to-right associate when several operators have the same precedence. For example, a / b * is illegal. Note that the definitions introduce factors and terms.

```
<expression> = <term> + <term> | <term> - <term>
<term> = <factor>* <factor> | <factor> / <factor>
<factor> = <letter> | <expression>
<letter> = a | b | ... | z
```

The recognition algorithm is based on a recursive chain of subtasks: find an expression. What makes this recursive chain is that find an expression uses a term, which in turn finds a factor. A factor either detects a base case or uses an expression, forming the recursive chain. The pseudocode for the recognition algorithm follows:

```
FIND AN EXPRESSION
// The grammar specifies that an expression is either a single term
// or a term followed by a * or a -, which must be followed by a second term.
```

```
Find a term
if (the next symbol is * or -)
Find a factor
```

```
FIND A TERM
// The grammar specifies that a term is either a single factor or
// a factor followed by a * or a /, which must be followed by a second factor.
```

```
Find a factor
if (the next symbol is * or /)
Find a factor
```

```
FIND A FACTOR
// The grammar specifies that a factor is either a letter (the base case) or
// an expression enclosed in parentheses.
```

```
if (the first symbol is a letter)
Done
else if (the first symbol is a '('
{
Find an expression starting at the character after '('
Check for ')'
}
else
No factors exists
```

Design and implement a class of infix expressions, as described by the given grammar. Include a method to recognize a legal infix expression.