
### 12.3.1 Syntactic Domains

Syntactic domains are defined in a denotational definition using notation that is almost identical to the abstract syntax described in Section 12.1. The sets being defined are listed first with capital letters denoting elements from the sets. Then the grammar rules are listed that recursively define the elements of the set. For example, the syntactic domains Number and Digit are specified as follows:

```
D: Digit
N: Number

N → N D | D
D → ‘0’ | ‘1’ | … | ‘9’
```

A denotational definition views the syntactic domains as sets of syntax trees whose structure is given by the grammar rules. Semantic functions will be defined recursively on these sets, based on the structure of a syntax tree node.

### 12.3.2 Semantic Domains

Semantic domains are the sets in which semantic functions take their values. These are sets like syntactic domains, but they also may have additional mathematical structure, depending on their use. For example, the integers have the arithmetic operations “+,” “−,” and “*.” Such domains are **algebras**, which need to be specified by listing their functions and properties. A denotational definition of the semantic domains lists the sets and the operations but usually omits the properties of the operations. These can be specified by the algebraic techniques studied in Chapter 11, or they can simply be assumed to be well known, as in the case of the arithmetic operations on the integers. A specification of the semantic domains also lists only the basic domains without specifically including domains that are constructed of functions on the basic domains.

Domains sometimes need special mathematical structures that are the subject of **domain theory** in programming language semantics. In particular, the term “domain” is sometimes reserved for an algebra with the structure of a complete partial order. Such a structure is needed to define the semantics of recursive functions and loops. See the references at the end of the chapter for further detail on domain theory.

An example of a specification of a semantic domain is the following specification of the integers:

```
Domain ν: Integer = { . . . , −2, −1, 0, 1, 2, . . . }
Operations
    + : Integer × Integer → Integer
    − : Integer × Integer → Integer
    * : Integer × Integer → Integer
```

In this example, we restrict ourselves to the three operations “+,” “−,” and “*,” which are the only operations represented in our sample language. In the foregoing notation, the symbols “ν” in the first line indicate that the name ν will be used for a general element from the domain, that is, an arbitrary integer.

### 12.3.3 Semantic Functions

A semantic function is specified for each syntactic domain. Each semantic function is given a different name based on its associated syntactic domain. A common convention is to use the boldface letter corresponding to the elements in the syntactic domain. Thus, the value function from the syntactic domain Digit to the integers is written as follows:

**D** : Digit → Integer

The value of a semantic function is specified recursively on the trees of the syntactic domains using the structure of the grammar rules. This is done by giving a semantic equation corresponding to each grammar rule.

For example, the grammar rules for digits

```
D → '0' | '1' | ... | '9'
```

give rise to the syntax tree nodes

```
D        D                  D
|        |       ...        |
'0'      '1'                '9'
```

and the semantic function **D** is defined by the following semantic equations:

```
    D                   D                            D
D(  |  ) = 0,    D(  |  ) = 1, ...,         D(  |  ) = 9
   '0'                 '1'                          '9'
```

representing the value of each leaf.

This cumbersome notation is shortened to the following:

**D**[['0']] = 0, **D**[['1']] = 1, ..., **D**[['9']] = 9

The double brackets [[...]] indicate that the argument is a syntactic entity consisting of a syntax tree node with the listed arguments as children.

As another example, the semantic function

```
N : Number → Integer
```

from numbers to integers is based on the syntax

```
N → N D | D
```

and is given by the following equations:

```
N[[ND]] = 10 * N[[N]] + N[[D]]
N[[D]] = D[[D]]
```

Here `[[ND]]` refers to the tree node

```
  N
 / \
N   D
```

and `[[D]]` refers to the node

```
N
|
D
```

We are now ready to give a complete denotational definition for the expression language of Section 12.1.

### 12.3.4 Denotational Semantics of Integer Arithmetic Expressions

Here is the denotational definition according to the conventions just described.

**Syntactic Domains**

```
E: Expression
N: Number
D: Digit

E → E₁ ‘+’ E₂ | E₁ ‘−’ E₂ | E₁ ‘*’ E₂
  | ‘(’ E ‘)’ | N
N → N D | D
D → ‘0’ | ‘1’ | … | ‘9’
```

**Semantic Domains**

```
Domain ν: Integer = { . . . , −2, −1, 0, 1, 2, . . . }
Operations
  + : Integer × Integer → Integer
  − : Integer × Integer → Integer
  * : Integer × Integer → Integer
```

**Semantic Functions**

```
E : Expression → Integer

E[[E₁ ‘+’ E₂]] = E[[E₁]] + E[[E₂]]
E[[E₁ ‘−’ E₂]] = E[[E₁]] − E[[E₂]]
E[[E₁ ‘*’ E₂]] = E[[E₁]] * E[[E₂]]
E[[‘(’ E ‘)’]] = E[[E]]
E[[N]] = N[[N]]

N : Number → Integer

N[[ND]] = 10 * N[[N]] + N[[D]]
N[[D]] = D[[D]]

D : Digit → Integer

D[[‘0’]] = 0, D[[‘1’]] = 1, . . . , D[[‘9’]] = 9
```

In this denotational description, we have retained the use of quotation marks to distinguish syntactic from semantic entities. In denotational semantics, this is not as necessary as in other semantic descriptions, since arguments to semantic functions are always syntactic entities. Thus, we could drop the quotation marks and write D[[0]] = 0, and so on. For clarity, we will generally continue to use the quotation marks, however.

To see how these equations can be used to obtain the semantic value of an expression, we compute `E[[(2 + 3)*4]]` or, more precisely, `E[[ ‘(’ ‘2’ ‘+’ ‘3’ ‘)’ ‘*’ ‘4’ ]]`:

```
E[[ ‘(’ ‘2’ ‘+’ ‘3’ ‘)’ ‘*’ ‘4’ ]]
= E[[ ‘(’ ‘2’ ‘+’ ‘3’ ‘)’ ]] * E[[ ‘4’ ]]
= E[[ ‘2’ ‘+’ ‘3’ ]] * N[[ ‘4’ ]]
= (E[[ ‘2’ ]] + E[[ ‘3’ ]]) * D[[ ‘4’ ]]
= (N[[ ‘2’ ]] + N[[ ‘3’ ]]) * 4
= (D[[ ‘2’ ]] + D[[ ‘3’ ]]) * 4
= (2 + 3) * 4 = 5 * 4 = 20
```

### 12.3.5 Environments and Assignment

The first extension to our basic sample language adds identifiers, assignment statements, and environments to the semantics. Environments are functions from identifiers to integers (or undefined), and the set of environments becomes a new semantic domain:

```
Domain Env: Environment = Identifier → Integer ∪ {undef}
```

In denotational semantics the value undef is given a special name, bottom, taken from the theory of partial orders, and is denoted by a special symbol, ⊥. Semantic domains with this special value added are called lifted domains and are subscripted with the symbol ⊥. Thus, `Integer ∪ {⊥}` is written as `Integer⊥`. The initial environment Env₀ defined in Section 12.1, in which all identifiers have undefined values, can now be defined as `Env₀(I) = ⊥` for all identifiers I.

The evaluation of expressions in the presence of an environment must include an environment as a parameter, so that identifiers may be associated with integer values. Thus, the semantic value of an expression becomes a function from environments to integers:

```
E : Expression → Environment → Integer⊥
```

In particular, the value of an identifier is its value in the environment provided as a parameter:

```
E[[I]](Env) = Env(I)
```

In the case of a number, the environment is immaterial:

```
E[[N]](Env) = N[[N]]
```

In other expression cases the environment is simply passed on to subexpressions.

To extend the semantics to statements and statement lists, we note that the semantic values of these constructs are functions from environments to environments. An assignment statement changes the environment to add the new value assigned to the identifier; in this case, we will use the same “&” notation for adding values to functions that we have used in previous sections. Now a statement-list is simply the composition of the functions of its individual statements (recall that the composition f ∘ g of two functions f and g is defined by (f ∘ g)(x) = f(g(x)). A complete denotational definition of the extended language is given in Figure 12.5.
