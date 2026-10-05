for an implementation-defined manner. if this search is not supported, or if the search
ails, the directive is reprocessed if it is read

```
# include <h-char-sequence> new-line
```

with the identical contained sequence (including > characters, if any) from the original
directive.

4 A preprocessing directive of the form

```
# include pp-tokens new-line
```

(that does not match one of the two previous forms) is permitted. The preprocessing
tokens after include in the directive are processed just as in normal text. (Each
identifier clearly defined as a macro is replaced by its replacement list of
preprocessing tokens.) The directive resulting after all replacements shall match one of
the two previous forms.¹⁷⁰) The method by which a sequence of preprocessing tokens
bween a < and a > preprocessing token pair or a pair of " characters is combined into a
single header name preprocessing token is implementation-defined.

5 The implementation shall provide unique mappings for sequences consisting of one or
more nondigits or digits (6.4.2.1) followed by a period (.) and a single nondigit.
The first character shall not be a digit. The implementation may ignore distinctions of
alphabetic case and restrict the mapping to eight significant characters before the
period.

6 A #include preprocessing directive may appear in a source file that has been read
because of a #include directive in another file, up to an implementation-defined
nesting limit (see 5.2.4.1).

7 EXAMPLE 1 The most common uses of #include preprocessing directives are as in the following:

```
#include <stdio.h>
#include "myprog.h"
```