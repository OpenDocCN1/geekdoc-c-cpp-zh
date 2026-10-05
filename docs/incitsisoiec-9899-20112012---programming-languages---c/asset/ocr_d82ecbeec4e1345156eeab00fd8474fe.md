# 6.10.9 Pragma operator

Semantics

1 A unary operator expression of the form:

```
_Pragma ( string-literal )
```

is processed as follows: The string literal *destringized* by deleting any encoding prefix, deleting the leading and trailing double-quotes, replacing each escape sequence \" by a double-quote, replacing each escape sequence \\ by a single backslash. The resulting sequence of characters is processed through translation phase 3 to produce preprocessing tokens that are executed as if they were the pp-tokens in a pragma directive. The original four preprocessing tokens in the unary operator expression are removed.

2 A directive of the form:

```
#pragma listing on "..\listing.dir"
```

can also be expressed as:

```
_Pragma ( "listing on \\\..listing.dir\" )
```

The latter is processed in the same way whether it appears literally as shown, or results from macro replacement, as in:

```
#define LISTING(x) PRAGMA(listing on #x)
#define PRAGMA(x) _Pragma (#x)
LISTING ( ..\listing.dir )
```