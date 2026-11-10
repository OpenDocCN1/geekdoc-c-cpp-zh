
## 2.2. SYNTAX DEFINITION

### Tokens Versus Terminals

In a compiler, the lexical analyzer reads the characters of the source program, groups them into lexically meaningful units called lexemes, and produces as output tokens representing these lexemes. A token consists of two components, a token name and an attribute value. The token names are abstract symbols that are used by the parser for syntax analysis. Often, we shall call these token names *terminals*, since they appear as terminal symbols in the grammar for a programming language. The attribute value, if present, is a pointer to the symbol table that contains additional information about the token. This additional information is not part of the grammar, so in our discussion of syntax analysis, often we refer to tokens and terminals synonymously.

terminals and/or nonterminals, called the *body* or *right side* of the production. The intuitive intent of a production is to specify one of the written forms of a construct; if the head nonterminal represents a construct, then the body represents a written form of the construct.

- 4. A designation of one of the nonterminals as the *start* symbol.

We specify grammars by listing their productions, with the productions for the start symbol listed first. We assume that digits, signs such as < and <=, and boldface strings such as **while** are terminals. An italicized name is a nonterminal, and any nonitalicized name or symbol may be assumed to be a terminal.^1 For notational convenience, productions with the same nonterminal as the head can have their bodies grouped, with the alternative bodies separated by the symbol |, which we read as “or.”

**Example 2.1:** Several examples in this chapter use expressions consisting of digits and plus and minus signs; e.g., strings such as 9-5+2, 3-1, or 7. Since a plus or minus sign must appear between two digits, we refer to such expressions as “lists of digits separated by plus or minus signs.” The following grammar describes the syntax of these expressions. The productions are:

```
list  ->  list + digit              (2.1)
list  ->  list - digit              (2.2)
list  ->  digit                     (2.3)
digit ->  0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  (2.4)
```

^1Individual italic letters will be used for additional purposes, especially when grammars are studied in detail in Chapter 4. For example, we shall use *X*, *Y*, and *Z* to talk about a symbol that is either a terminal or a nonterminal. However, any italicized name containing two or more characters will continue to represent a nonterminal.

The bodies of the three productions with nonterminal *list* as head equivalently can be grouped:

```
list -> list + digit | list - digit | digit
```

According to our conventions, the terminals of the grammar are the symbols

```
+ - 0 1 2 3 4 5 6 7 8 9
```

The nonterminals are the italicized names *list* and *digit*, with *list* being the start symbol because its productions are given first. □

We say a production is *for* a nonterminal if the nonterminal is the head of the production. A string of terminals is a sequence of zero or more terminals. The string of zero terminals, written as ε, is called the *empty string*.²

²Technically, ε can be a string of zero symbols from any alphabet (collection of symbols).

### 2.2.2 Derivations

A grammar derives strings by beginning with the start symbol and repeatedly replacing a nonterminal by the body of a production for that nonterminal. The terminal strings that can be derived from the start symbol form the *language* defined by the grammar.

**Example 2.2:** The language defined by the grammar of Example 2.1 consists of lists of digits separated by plus and minus signs. The ten productions for the nonterminal *digit* allow it to stand for any of the terminals 0, 1, ..., 9. From production (2.3), a single digit by itself is a list. Productions (2.1) and (2.2) express the rule that any list followed by a plus or minus sign and then another digit makes up a new list.

Productions (2.1) to (2.4) are all we need to define the desired language. For example, we can deduce that 9-5+2 is a *list* as follows.

- a) 9 is a *list* by production (2.3), since 9 is a *digit*.
- b) 9-5 is a *list* by production (2.2), since 9 is a *list* and 5 is a *digit*.
- c) 9-5+2 is a *list* by production (2.1), since 9-5 is a *list* and 2 is a *digit*.

□

**Example 2.3:** A somewhat different sort of list is the list of parameters in a function call. In Java, the parameters are enclosed within parentheses, as in the call max(x,y) of function max with parameters x and y. One nuance of such lists is that an empty list of parameters may be found between the terminals ( and ). We may start to develop a grammar for such sequences with the productions:

```
call       →  id ( optparams )
optparams  →  params | ε
params     →  params , param | param
```

Note that the second possible body for *optparams* ("optional parameter list") is ε, which stands for the empty string of symbols. That is, *optparams* can be replaced by the empty string, so a *call* can consist of a function name followed by the two-terminal string (). Notice that the productions for *params* are analogous to those for *list* in Example 2.1, with comma in place of the arithmetic operator + or −, and *param* in place of *digit*. We have not shown the productions for *param*, since parameters are really arbitrary expressions. Shortly, we shall discuss the appropriate productions for the various language constructs, such as expressions, statements, and so on. □

*Parsing* is the problem of taking a string of terminals and figuring out how to derive it from the start symbol of the grammar, and if it cannot be derived from the start symbol of the grammar, then reporting syntax errors within the string. Parsing is one of the most fundamental problems in all of compiling; the main approaches to parsing are discussed in Chapter 4. In this chapter, for simplicity, we begin with source programs like `9-5+2` in which each character is a terminal; in general, a source program has alphanumeric lexemes that are grouped by the lexical analyzer into tokens, whose first components are the terminals processed by the parser.

### 2.2.3 Parse Trees

A parse tree pictorially shows how the start symbol of a grammar derives a string in the language. If nonterminal A has a production `A → XYZ`, then a parse tree may have an interior node labeled A with three children labeled X, Y, and Z, from left to right:

![](img/a29d16e454785bb105e96ef448ac07f6_49_0.png)

Formally, given a context-free grammar, a *parse tree* according to the grammar is a tree with the following properties:

- 1. The root is labeled by the start symbol.
- 2. Each leaf is labeled by a terminal or by ε.
- 3. Each interior node is labeled by a nonterminal.
- 4. If A is the nonterminal labeling some interior node and X₁, X₂, …, Xₙ are the labels of the children of that node from left to right, then there must be a production A → X₁X₂ ··· Xₙ. Here, X₁, X₂, …, Xₙ each stand for a symbol that is either a terminal or a nonterminal. As a special case, if *A* → ε is a production, then a node labeled *A* may have a single child labeled ε.

### Tree Terminology

Tree data structures figure prominently in compiling.

- A tree consists of one or more *nodes*. Nodes may have *labels*, which in this book typically will be grammar symbols. When we draw a tree, we often represent the nodes by these labels only.
- Exactly one node is the *root*. All nodes except the root have a unique *parent*; the root has no parent. When we draw trees, we place the parent of a node above that node and draw an edge between them. The root is then the highest (top) node.
- If node *N* is the parent of node *M*, then *M* is a *child* of *N*. The children of one node are called *siblings*. They have an order, *from the left*, and when we draw trees, we order the children of a given node in this manner.
- A node with no children is called a *leaf*. Other nodes — those with one or more children — are *interior nodes*.
- A *descendant* of a node *N* is either *N* itself, a child of *N*, a child of a child of *N*, and so on, for any number of levels. We say node *N* is an *ancestor* of node *M* if *M* is a descendant of *N*.

**Example 2.4:** The derivation of 9-5+2 in Example 2.2 is illustrated by the tree in Fig. 2.5. Each node in the tree is labeled by a grammar symbol. An interior node and its children correspond to a production; the interior node corresponds to the head of the production, the children to the body.

In Fig. 2.5, the root is labeled *list*, the start symbol of the grammar in Example 2.1. The children of the root are labeled, from left to right, *list*, +, and *digit*. Note that

*list* → *list* + *digit*

is a production in the grammar of Example 2.1. The left child of the root is similar to the root, with a child labeled - instead of +. The three nodes labeled *digit* each have one child that is labeled by a digit. □

From left to right, the leaves of a parse tree form the *yield* of the tree, which is the string *generated* or *derived* from the nonterminal at the root of the parse tree.
