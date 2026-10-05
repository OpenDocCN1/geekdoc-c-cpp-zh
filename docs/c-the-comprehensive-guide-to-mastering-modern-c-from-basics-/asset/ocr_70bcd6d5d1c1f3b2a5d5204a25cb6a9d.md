Much more relevant, however, is switch(c). As a char,
y can use c here, just like int and its relatives.
However, you must not write a double or string here. It
must be an "enumerable" type.

The case follow one after another. Depending on
t value of c, these jump labels are directly accessed,
and the subsequent statements are executed. Each
block is properly concluded with a break; to prevent
accidentally executing another calculation.

A small comment on the calculation c-'0': Here, I
ubtract the character value '0' from the entered c to
get the numeric value of the character. Mind you, this is
not the int number 0, but the char character '0'. The
result is int number between 0 and 9. This works
partly because char behaves very much like an integer
type and partly because the characters '0' to '9' have
consecutive values as int. The '0' usually has the
number 48 and the '4' (for example) the value 52. Thus,
'4'-'0' is the same as 52-48, which is the int 4. I then put
this numeric value onto the stack.

# It Can Be Better; It Can Be Dynamic

The char-based switch is quite nice as a small
example, but it is very static and can become
unwieldy when you want to extend it. However, if
you want to see a version that is better suited as a
basis for an elaborate calculator, flip far ahead to
Chapter 28, Listing 28.43. There, it is a dynamic
that takes function objects for the operations.