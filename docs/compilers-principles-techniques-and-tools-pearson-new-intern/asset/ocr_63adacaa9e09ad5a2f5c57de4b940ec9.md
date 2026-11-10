by applying *gen* to a combination of expressions and strings.

When we translate the production E → E₁ + E₂, the semantic rules in Fig. 6.19 build up E.code by concatenating E₁.code, E₂.code, and an instruction that adds the values of E₁ and E₂. The instruction puts the result of the addition into a new temporary name for E, denoted by E.addr.

The translation of E → -E₁ is similar. The rules create a new temporary for E and generate an instruction to perform the unary minus operation.

Finally, the production S → id = E; generates instructions that assign the value of expression E to the identifier id. The semantic rule for this production uses function top_get to determine the address of the identifier represented by id, as in the rules for E → id. S.code consists of the instructions to compute the value of E into an address given by E.addr, followed by an assignment to the address top_get(id.lexeme) for this instance of id.

**Example 6.11 :** The syntax-directed definition in Fig. 6.19 translates the assignment statement a = b + -c ; into the three-address code sequence

```
```
t₁ = minus c
t₂ = b + t₁
a = t₂
```
```

□

# ## 6.4.2 Incremental Translation

Code attributes can be long strings, so they are usually generated incrementally, as discussed in Section 5.5.2. Thus, instead of building up E.code as in Fig. 6.19, we can arrange to generate only the new three-address instructions, as in the translation scheme of Fig. 6.20. In the incremental approach, *gen* not only constructs a three-address instruction, it appends the instruction to the sequence of instructions generated so far. The sequence may either be retained in memory for further processing, or it may be output incrementally.

The translation scheme in Fig. 6.20 generates the same code as the syntax-directed definition in Fig. 6.19. With the incremental approach, the code attribute is not used, since there is a single sequence of instructions that is created by successive calls to *gen*. For example, the semantic rule for E → E₁ + E₂ in Fig. 6.20 simply calls *gen* to generate an add instruction; the instructions to compute E₁ into E₁.addr and E₂ into E₂.addr have already been generated.

The approach of Fig. 6.20 can also be used to build a syntax tree. The new semantic action for E → E₁ + E₂ creates a node by using a constructor, as in

```
```
E → E₁ + E₂   { E.addr = new Node('+', E₁.addr, E₂.addr); }
```
```

Here, attribute addr represents the address of a node rather than a variable or constant.

of generated instructions.