**Exercise 6.5.2:** As in Ada, suppose that each expression must have a unique type, but that from a subexpression by itself, all we can deduce is a set of possible types. That is, the application of function $E_1$ to argument $E_2$, represented by $E \rightarrow E_1(E_2)$, has the associated rule

$$E_1.\mathit{type} = \{\ t\mid\text{for some }s\text{ in }E_2.\mathit{type},\ s\rightarrow t\text{ is in }E_1.\mathit{type}\ \}$$

Describe an SDD that determines a unique type for each subexpression by using an attribute $\mathit{type}$ to synthesize a set of possible types bottom-up, and, once the unique type of the overall expression is determined, proceeds top-down to determine attribute $\mathit{unique}$ for the type of each subexpression.

# ## 6.6 Control Flow

The translation of statements such as if-else-statements and while-statements is tied to the translation of boolean expressions. In programming languages, boolean expressions are often used to

+   1. *Alter the flow of control.* Boolean expressions are used as conditional expressions in statements that alter the flow of control. The value of such boolean expressions is implicit in a position reached in a program. For example, in `if (E) S`, the expression $E$ must be true if statement $S$ is reached.
+   
+   2. *Compute logical values.* A boolean expression can represent *true* or *false* as values. Such boolean expressions can be evaluated in analogy to arithmetic expressions using three-address instructions with logical operators.

The intended use of boolean expressions is determined by its syntactic context. For example, an expression following the keyword if is used to alter the flow of control, while an expression on the right side of an assignment is used to denote a logical value. Such syntactic contexts can be specified in a number of ways: we may use two different nonterminals, use inherited attributes, or set a flag during parsing. Alternatively we may build a syntax tree and invoke different procedures for the two different uses of boolean expressions.

This section concentrates on the use of boolean expressions to alter the flow of control. For clarity, we introduce a new nonterminal $B$ for this purpose. In Section 6.6.6, we consider how a compiler can allow boolean expressions to represent logical values.

# ### 6.6.1 Boolean Expressions

Boolean expressions are composed of the boolean operators (which we denote `&&`, `||`, and `!`, using the C convention for the operators AND, OR, and NOT, respectively) applied to elements that are boolean or relational expressions. Relational expressions are of the form $E_1\ \mathit{rel}\ E_2$, where $E_1$ and