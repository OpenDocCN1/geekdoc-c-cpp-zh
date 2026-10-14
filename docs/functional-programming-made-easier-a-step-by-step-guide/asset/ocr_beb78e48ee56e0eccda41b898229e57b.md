① The operator <* ignores the result of right argument, i.e. it only relies on it's Side-effect, i.e. parse the character or characters.

While this form is just as valid, it's a bit clunky and has the burden of the Lambda Function, which makes this form less desirable, if you ask me. In the case where the Function is a Data Constructor, however, this form has its merits. You'll have to decide which you like better for each situation.

And just for fun, here's the version that just uses >>=:

```
uglyB :: ∀ e. ParserError e => Parser e (Array String)
uglyB =
  range' 1 4 digit
    >>= \p1 -> constChar ','
      >>= \_ -> constChar ' '
        >>= \_ -> some' (letter <|> constChar' ' ')
          >>= \p2 -> many' digit
            >>= \p3 -> pure [p1, p2, p3]
```

Notice that it's just a mechanical process to convert the do notation to >>=.

Also, notice, that everywhere that >>= is used, the error checks that we coded in bind for Parser get performed. This frees us up to code the Happy Path here.

Well, we could work on this parse for months, but we're going to have to put it away for now. Hopefully, this process has taught you that parsers are not magic. The existing libraries are just far more extensive versions of what we've built. But ours has most of the basic ideas.

Next time you need to parse some arbitrary String, you can comfortably reach for an Applicative or a Monadic Parsing Library in either PureScript or Haskell instead of relying on writing the hieroglyphics of Regular Expressions.

# 19.11. The RWS Monad

When we first learned about Monads, we went through the coding of Writer, Reader and State. We can now leverage these in programs that we write. But what if we want to have a Computation that writes a log and updates State? How do we combine Monads?

Combining different Monads is a subject for the next Chapter, but we can use the features of these 3 Monads today by just writing a combination Monad called RWS.

The first step in writing any Monad is to model its Type and to do that, we'll need to ask the all important question of what does the Type contain, a Value or a Function?

If you remember, Writer contains a Value and both Reader and State contain Functions. So, if we're going to write a combination Monad, we'll probably want the RWS Type to contain a Function.