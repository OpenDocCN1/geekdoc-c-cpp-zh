concepts;
§24.3.
[6] Do not give unconventional meaning to conventional notation; §24.3.
[7] Use concepts as a design tool; §24.3.
[8] Aim for “plug compatibility” among algorithms and argument type by using common and
regular template argument requirements; §24.3.
[9] Discover a concept by minimizing an algorithm’s requirements on its template arguments and
then generalizing for wider use; §24.3.1.
[10] A concept is not just a description of the needs of a particular implementation of an algorithm; §24.3.1.
[11] If possible, choose a concept from a list of well-known concepts; §24.3.1, §24.4.4.
[12] The default concept for a template argument is Regular; §24.3.1.
[13] Not all template argument types are Regular; §24.3.1.
[14] A concept requires a semantic aspect; it is not primarily a syntactic notion; §24.3.1, §24.3.2, §24.4.1.
[15] Make concepts concrete in code; §24.4.
[16] Express concepts as compile-time predicates (constexpr functions) and test them using static_assert() or enable_if<>; §24.4.
[17] Use axioms as a design tool; §24.4.1.
[18] Use axioms as a guide for testing; §24.4.1.
[19] Some concepts involve two or more template arguments; §24.4.2.
[20] Concepts are not just types of types; §24.4.2.
[21] Concepts can involve numeric values; §24.4.3.
[22] Use concepts as a guide for testing template definitions; §24.4.5.

This page intentionally left blank