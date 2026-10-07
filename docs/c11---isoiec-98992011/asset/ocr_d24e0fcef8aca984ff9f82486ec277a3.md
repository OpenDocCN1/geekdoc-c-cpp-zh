# ISO/IEC 9899:2011 (E)

"a" "b" "L"c"
"a" "L"b" "c"
L"a" "b" "L"c"
L"a" "L"b" "L"c"

Likewise, each of the sequences
"a" "b" "u"c"
"a" "u"b" "c"
u"a" "b" "u"c"
"u" "u"b" "u"c"

is equivalent to
uuabcabc"

**Forward references:** common definitions `<stddef.h>` (7.19), the **mbstowcs** function (72.2.8.1), Unicode units in `<uchar.h>` (7.28).

# 6.4.6 Punctuators

# Syntax

+   punctuator: one of
[ ] ( ) { } . ->
++ / & * + ~ !
/ % << >> > <= == != ^ && ||
? ;
* = / % += - <= >= &= = | =
# ##
< : > % % % : % ::

# Semantics

+   A punctuator is a symbol that has syntactic and semantic significance. Depending on context, it may specify an operation to be performed (which in turn may yield a value or a function designator, produce a side effect, or some combination thereof) in which case it is known as an *operator* (other forms of operator also exist in some contexts). An *operand* is an entity on which an operator acts.