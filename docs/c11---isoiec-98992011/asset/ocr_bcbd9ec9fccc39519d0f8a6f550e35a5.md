to 0. If the first substatement is reached via a label, the second substatement is not executed.

+   3 An else is associated with the lexically nearest preceding if that is allowed by the syntax.

# 6.8.4.2 The switch statement

# Constraints

+   1 The controlling expression of a switch statement shall have integer type.

+   2 If a switch statement has an associated case or default label within the scope of an identifier with a variably modified type, the entire switch statement shall be within the scope of that identifier.¹154)

+   3 The expression of each case label be an integer constant expression and no two of the case constant expressions in the same switch statement shall have the same value after conversion. There may be at most one default label in a switch statement. (Any enclosed switch statement may have a default label or case constant expressions with values that duplicate case constant expressions in the enclosing switch statement.)

# Semantics

+   4 A switch statement causes control to jump into, or to the part that the switch body, depending on the value of a controlling expression, and on the presence of a default label and the values of any case labels on or in the switch body. A case or default label is accessible only within the closest enclosing switch statement.

+   5 The integer motions are performed on the controlling expression. The expression in each case label is converted to the promoted type of the controlling expression. If a converted value matches that of the promoted controlling expression, control jumps to the statement following the matched case. Otherwise, if there is a default label, control jumps to the labeled statement. If no converted case constant expression matches and there is no default label, no part of the switch body is executed.

# Implementation limits

+   6 As discussed in 5.2.4.1, the implementation may limit the number of case values in a switch statement.

> 154) That is, the declaration either precedes the switch statement, or it follows the last case or default label associated with the switch that is in the block containing the declaration.

$6.8.4.2 Language 149