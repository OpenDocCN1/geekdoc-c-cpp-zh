# Appendix C
Language Definitions

This appendix is intended as a reference for definitions relevant to this book.

# C.1 Value Categories

C++ distinguishes among different categories of values. The most important are lvalue and rvalue.

Definition C-1 (lvalue). An lvalue (so called, historically, because lvalues can appear on the left-hand side of an assignment expression) designates a function or an object.

More pragmatically, an lvalue is an entity from which we can get an address. This does not exclude that they may be constant—although this is somewhat inconsistent with the terminology. The reason for this is that early versions of C had no const attribute so all lvalues were allowed on the left side of an assignment.

The counterpart is:

Definition C-2 (rvalue). An rvalue (so called, historically, because rvalues can appear on the right-hand side of an assignment expression) is an expired value (e.g., an object casted to an rvalue reference), a temporary object or sub-object thereof, or a value that is not associated with an object.

The definitions are adapted from the ISO standard.

# C.2 Operator Overview

| Description | Notation | Assoc. |
| :--- | :--- | :--- |
| Parenthesized expression | ( expr ) | – |
| Lambda | [ capture_list ] lambda_declarator { stmt_list } | – |
| Scope resolution | class_name :: member | – |
| Scope resolution | namespace_name :: member | – |
| Global namespace | :: name | – |
| Global namespace | :: qualified-name | (continues) |