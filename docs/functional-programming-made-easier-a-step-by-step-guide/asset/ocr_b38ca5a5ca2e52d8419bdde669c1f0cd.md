```
Warning found:
in module Text.Parsing.Parser
at .spago/parsing/v6.0.1/src/Text/Parsing/Parser.purs:117:1 - 117:64 (line 117, column 1 - line 117, column 64)

    A custom warning occurred while solving type class constraints:

        'MonadZero' is deprecated, use 'Monad' and 'Alternative' constraints instead

in value declaration monadZeroParserT

See
https://github.com/purescript/documentation/blob/master/errors/UserDefinedWarning.md for more information,
or to contribute content related to this warning.
```

Turns out that in version 14 of the PureScript compiler and subsequent libraries, MonadZero has been marked as deprecated. The purescript-parsing library has until version 15 to remove such use but has yet to do so. This warning can be safely ignored.

Next, let’s look at the Parser Monad from this library to better understand how we can use this: