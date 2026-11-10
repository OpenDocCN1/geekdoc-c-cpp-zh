by applying `gen` to a combination of expressions and strings.

When we translate the production $E \to E_1 + E_2$, the semantic rules in Fig. 6.19 build up `E.code` by concatenating `E₁.code`, `E₂.code`, and an instruction that adds the values of $E_1$ and $E_2$. The instruction puts the result of the addition into a new temporary name for $E$, denoted by `E.addr`.

The translation of $E \to -E_1$ is similar. The rules create a new temporary for $E$ and generate an instruction to perform the unary minus operation.

Finally, the production $S \to \text{id} = E$ generates instructions that assign the value of expression $E$ to the identifier `id`. The semantic rule for this production uses function `top.get` to determine the address of the identifier represented by `id`, as in the rules for $E \to \text{id}$. `S.code` consists of the instructions to compute the value of $E$ into an address given by `E.addr`, followed by an assignment to the address `top.get(id.lexeme)` for this instance of `id`.

**Example 6.11:** The syntax-directed definition in Fig. 6.19 translates the assignment statement $a = b + -c;$ into the three-address code sequence

```
t₁ = minus c
t₂ = b + t₁
a = t₂
```

# 6.4.2  Incremental Translation

Code attributes can be long strings, so they are usually generated incrementally, as discussed in Section 5.5.2. Thus, instead of building up `E.code` as in Fig. 6.19, we can arrange to generate only the new three-address instructions, as in the translation scheme of Fig. 6.20. In the incremental approach, `gen` not only constructs a three-address instruction, it appends the instruction to the sequence of instructions generated so far. The sequence may either be retained in memory for further processing, or it may be output incrementally.

The translation scheme in Fig. 6.20 generates the same code as the syntax-directed definition in Fig. 6.19. With the incremental approach, the code attribute is not used, since there is a single sequence of instructions that is created by successive calls to `gen`. For example, the semantic rule for $E \to E_1 + E_2$ in Fig. 6.20 simply calls `gen` to generate an add instruction; the instructions to compute $E_1$ into $E_1.addr$ and $E_2$ into $E_2.addr$ have already been generated.

The approach of Fig. 6.20 can also be used to build a syntax tree. The new semantic action for $E \to E_1 + E_2$ creates a node by using a constructor, as in

```
E → E₁ + E₂   { E.addr = new Node('+', E₁.addr, E₂.addr); }
```

Here, attribute `addr` represents the address of a node rather than a variable or constant.

of generated instructions.