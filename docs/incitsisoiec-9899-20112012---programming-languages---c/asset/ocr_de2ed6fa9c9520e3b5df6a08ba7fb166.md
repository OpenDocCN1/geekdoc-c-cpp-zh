# 6.6 Constant expressions

# Syntax

constant-expression:
    conditional-expression

# Description

A constant expression can be evaluated during translation rather than runtime, and accordingly may be used in any place that a constant may be.

# Constraints

Constant expressions shall not contain assignment, increment, decrement, function-call, or comma operators, except when they are contained within a subexpression that is not evaluated.^{115}

Each constant expression shall evaluate to a constant that is in the range of representable values for its type.

# Semantics

An expression that evaluates to a constant is required in several contexts. If a floating expression is evaluated in the translation environment, the arithmetic environment and precision shall be at least as great as if the expression were being evaluated in the execution environment.^{116}

An integer constant expression^{117} shall have integer type and shall only have operands that are integer constants, enumeration constants, character constants, **sizeof** expressions whose results are integer constants, **_Alignof** expressions, and floating constants that are the immediate operands of casts. Cast operators in an integer constant expression shall only convert arithmetic types to integer types, except as part of an operand to the **sizeof** or **_Alignof** operator.

More latitude is permitted for constant expressions in initializers. Such a constant expression shall be, or evaluate to, one of the following:

+   - an arithmetic constant expression,

115) The operand of a **sizeof** or **_Alignof** operator is usually not evaluated (6.5.3.4).

116) The use of evaluation formats as characterized by **FLT_EVAL_METHOD** also applies to evaluation in the translation environment.

117) An integer constant expression is required in a number of contexts such as the size of a bit-field member of a structure, the value of an enumeration constant, and the size of a non-variable array. Further constraints apply to the integer constant expressions used in conditional-inclusion preprocessor directives are discussed in 6.10.1.