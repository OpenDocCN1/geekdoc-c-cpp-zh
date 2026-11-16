based descendant, CLASSIC (Brachman 91). Many others have been proposed including visual-based languages.

As described in Chapter 1, rules are commonly used as the knowledge base in expert systems since their advantages greatly outweigh their disadvantages.

One formal notation for defining productions is the Backus-Naurform (BNF). This notation is a metalanguage for defining the syntax of a language. Syntax defines the form, while semantics refers to meaning. A metalanguage is a language for describing languages. Since the prefix meta means above, a metalanguage is above normal language.

There are many types of languages such as natural languages, logic languages, mathematics, and computer languages. The BNF notation for a simple English language rule that a sentence consists of a noun and a verb followed by ending punctuation is given as the following production rule:

```
<sentence> ::= <subject> <verb> <end-mark>
```

where the angle brackets, <>, and ::= are symbols of the metalanguage and not of the language being specified. The symbol ::= means "is defined as" and is the BNF equivalent of the arrow, =>, used in Chapter 1 with production rules.

The terms within angle brackets are called nonterminal symbols or simply nonterminals. A nonterminal is a variable that represents another term. The other term may be a nonterminal or a terminal. A terminal cannot be replaced by anything else and so is a constant.

The nonterminal <sentence> is special because it is the one start symbol from which the other sentences are defined. In the definition of programming languages, the start symbol is usually named <program>. The production rule:

```
<sentence> -> <subject> <verb> <end-mark>
```

states that a sentence is composed of a subject, followed by a verb, followed by an end-mark. The following rules complete the nonterminals by specifying their possible terminals. The bar means "or" in the metalanguage:

```
<subject> -> I | You | We
<verb> -> left | came
<end-mark> -> . | ? | !
```

All possible sentences in the language, i.e., the productions, can be produced by successively replacing each nonterminal by its right-hand-side nonterminals or terminals until all nonterminals are eliminated. The following are some productions:

```
I left.
I left?
I left!
```