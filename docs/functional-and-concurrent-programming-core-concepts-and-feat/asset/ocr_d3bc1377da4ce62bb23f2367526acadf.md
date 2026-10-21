This function proceeds by repeatedly adding the head of the list being reversed to the front of an accumulator list `rev`. You can think of it as peeling cards from a deck and putting them onto the table: In the end, the resulting deck of cards is the reverse of the original deck.

Contrary to the previous attempt, this implementation only uses “::” directly to build the resulting list, and is linear in complexity. As a simple experiment on the desktop computer used to typeset this book, it took approximately 75 milliseconds to reverse a list of 5000 numbers using the first implementation. This time decreased to 0.027 millisecond when the improved variant was used, a more than 1/2000 reduction. Incidentally, this implementation has also become tail recursive, and can handle lists of arbitrary length.

There may be situations where you are tempted to append to a list because prepending would not produce a list in the right order. Don’t do it. Instead, build the list in the wrong order, efficiently, and then reverse it. For instance, to extract space-separated tokens from a stream of characters, it would feel natural to use append to add a character to the current token, then append again to add a token to a list of tokens. Instead, you can use a combination of prepending and reversing:

```
```scala
def tokenize(stream: List[Char]): List[String] =
  def addToken(token: List[Char], tokens: List[String]): List[String] =
    if isEmpty(token) then tokens else reverse(token).mkString :: tokens

  @tailrec
  def loop(stream: List[Char], token: List[Char], tokens: List[String]): List[String]=
    stream match
      case w :: chars if w.isWhitespace => loop(chars, Nil, addToken(token, tokens))
      case c :: chars                  => loop(chars, c :: token, tokens)
      case Nil                          => addToken(token, tokens)

  reverse(loop(stream, Nil, Nil))
```
```

Characters are processed one at a time in function `loop`. A non-whitespace character (c) is added to the current token, and the computation proceeds recursively. Upon encountering a whitespace character (w), the current token is added to a list of tokens, and a new token (Nil) is started. The last token, which is not necessarily followed by whitespace, is added at the end.

Note how characters are added to tokens using constant-time operation “::”. As a result, tokens are built in reverse order. In function `addToken`, each token is reversed one time when it is added to the list. (The function skips empty tokens and uses standard method `mkString` to convert a list of characters into a string.) Similarly, tokens are added to a list of tokens using “::”, and the list is reversed at the end. Since reversal was implemented in linear time, the entire tokenization time remains proportional to the lengths and number of tokens.