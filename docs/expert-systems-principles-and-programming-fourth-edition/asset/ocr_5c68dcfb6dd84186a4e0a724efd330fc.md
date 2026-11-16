<instance-name-list> ::= <instance-name>+ | ?VARIABLE
<value-list> ::= <constant>+ | ?VARIABLE
<range-attribute> ::= (range <range-specification>)
<range-specification> ::= <number> | ?VARIABLE
<cardinality-attribute> ::= (cardinality <cardinality-specification>)
<cardinality-specification> ::= <integer> | ?VARIABLE

# Variables and Expressions

<single-field-variable> ::= ?<variable-symbol>
<multifield-variable> ::= $?<variable-symbol>
<global-variable> ::= ?*<symbol>*
<variable> ::= <single-field-variable> | <multifield-variable> | <global-variable>
<function-call> ::= (<function-name> <expression>*) | (<special-function-name> <special-function-arguments>)
<special-function-name> ::= The name of a function such as assert or make-instance that does not parse its arguments in the default manner that standard functions use.
<special-function-arguments> ::= Argument parsing for special functions varies. Refer to the documentation for each special function for its valid syntax. For example, in the function (assert <relation>), the relation value (3) is a call to the function with an argument of 3, it is the fact to be asserted.
<expression> ::= <constant> | <variable> | <function-call>

# Data Types

<symbol> ::= A valid symbol as specified in Section 7.4
<string> ::= A valid string as defined in Section 7.4
<float> ::= A valid float as defined in Section 7.4
<integer> ::= A valid integer as specified in Section 7.4