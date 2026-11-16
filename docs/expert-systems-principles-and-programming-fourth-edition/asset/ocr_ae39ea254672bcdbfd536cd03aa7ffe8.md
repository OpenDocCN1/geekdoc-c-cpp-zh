```
```
<default-attribute>
 ::= (default ?DERIVE | ?NONE | <expression>*) |
 (default-dynamic <expression>*)
```
```

# Fact Specification

```
```
<RHS-pattern> ::= <ordered-RHS-pattern> |
 <template-RHS-pattern>
<ordered-RHS-pattern> ::= (<symbol> <RHS-field>+)
<template-RHS-pattern> ::= (<deftemplate-name>
 <RHS-slot>*)
<RHS-slot> ::= <single-field-RHS-slot> |
 <multifield-RHS-slot>
<single-field-RHS-slot> ::= (<slot-name> <RHS-field>)
<multifield-RHS-slot> ::= (<slot-name> <RHS-field>*)
.
<RHS-field> ::= <variable> |
 <constant> |
 <function-call>
```
```

# Defrule Construct

```
```
<defrule-construct> ::= (defrule <name> [<comment>]
 . [<declaration>]
 <conditional-element>*
 =>
 <expression>*)
<declaration> ::= (declare <rule-property>+)
<rule-property>
 ::= (salience <integer-expression>) |
 (auto-focus <boolean-symbol>)
<boolean-symbol> ::= TRUE | FALSE
<conditional-element> ::= <pattern-CE> |
 <assigned-pattern-CE> |
 <not-CE> |
 <and-CE> |
 <or-CE> |
 <logical-CE> |
 <test-CE> |
 <exists-CE> |
 <forall-CE>
<pattern-CE> ::= <ordered-pattern-CE> |
 <template-pattern-CE> |
 <object-pattern-CE>
<assigned-pattern-CE>
 ::= <single-field-variable> <- <pattern-CE>
<not-CE> ::= (not <conditional-element>)
<and-CE> ::= (and <conditional-element>+)
```
```