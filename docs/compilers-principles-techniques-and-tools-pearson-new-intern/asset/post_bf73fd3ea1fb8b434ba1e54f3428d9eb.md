
The translation in (b) shows position numbers for the instructions, starting arbitrarily at position 100. In both translations, the last instruction is a conditional jump to the first instruction. The multiplication `i * 8` is appropriate for an array of elements that each take 8 units of space.

![](img/a29d16e454785bb105e96ef448ac07f6_370_0.png)

(a) Symbolic labels.

(b) Position numbers.

Figure 6.9: Two ways of assigning labels to three-address statements

The choice of allowable operators is an important issue in the design of an intermediate form. The operator set clearly must be rich enough to implement the operations in the source language. Operators that are close to machine instructions make it easier to implement the intermediate form on a target machine. However, if the front end must generate long sequences of instructions for some source-language operations, then the optimizer and code generator may have to work harder to rediscover the structure and generate good code for these operations.

## 6.2.2 Quadruples

The description of three-address instructions specifies the components of each type of instruction, but it does not specify the representation of these instructions in a data structure. In a compiler, these instructions can be implemented as objects or as records with fields for the operator and the operands. Three such representations are called “quadruples,” “triples,” and “indirect triples.” A *quadruple* (or just “quad”) has four fields, which we call `op`, `arg₁`, `arg₂`, and `result`. The `op` field contains an internal code for the operator. For instance, the three-address instruction `x = y + z` is represented by placing `+` in `op`, `y` in `arg₁`, `z` in `arg₂`, and `x` in `result`. The following are some exceptions to this rule:

- Instructions with unary operators like `x = minus y` or `x = y` do not use `arg₂`. Note that for a copy statement, like `x = y`, `op` is `=`, while for most other operations, the assignment operator is implied.
- Operators like `param` use neither `arg₂` nor `result`.
- Conditional and unconditional jumps put the target label in `result`.

**Example 6.6:** Three-address code for the assignment `a = b * -c + b * -c` appears in Fig. 6.10(a). The special operator `minus` is used to distinguish the unary minus operator, as in `-c`, from the binary minus operator, as in `b - c`. Note that the unary-minus “three-address” statement has only two addresses, as does the copy statement `a = t₅`.

The quadruples in Fig. 6.10(b) implement the three-address code in (a).

```
t₁ = minus c
t₂ = b * t₁
t₃ = minus c
t₄ = b * t₃
t₅ = t₂ + t₄
a = t₅
```

|   | op | arg₁ | arg₂ | result |
|---|---|---|---|---|
| 0 | `minus` | `c` |  | `t₁` |
| 1 | `*` | `b` | `t₁` | `t₂` |
| 2 | `minus` | `c` |  | `t₃` |
| 3 | `*` | `b` | `t₃` | `t₄` |
| 4 | `+` | `t₂` | `t₄` | `t₅` |
| 5 | `=` | `t₅` |  | `a` |
|   | … |  |  |  |

(a) Three-address code

(b) Quadruples

Figure 6.10: Three-address code and its quadruple representation

For readability, we use actual identifiers like a, b, and c in the fields `arg₁`, `arg₂`, and `result` in Fig. 6.10(b), instead of pointers to their symbol-table entries. Temporary names can either be entered into the symbol table like programmer-defined names, or they can be implemented as objects of a class `Temp` with its own methods.

## 6.2.3 Triples

A triple has only three fields, which we call `op`, `arg₁`, and `arg₂`. Note that the `result` field in Fig. 6.10(b) is used primarily for temporary names. Using triples, we refer to the result of an operation `op` by its position, rather than by an explicit temporary name. Thus, instead of the temporary `t₁` in Fig. 6.10(b), a triple representation would refer to position (0). Parenthesized numbers represent pointers into the triple structure itself. In Section 6.1.2, positions or pointers to positions were called value numbers.

Triples are equivalent to signatures in Algorithm 6.3. Hence, the DAG and triple representations of expressions are equivalent. The equivalence ends with expressions, since syntax-tree variants and three-address code represent control flow differently.

**Example 6.7:** The syntax tree and triples in Fig. 6.11 correspond to the three-address code and quadruples in Fig. 6.10. In the triple representation in Fig. 6.11(b), the copy statement `a = t₅` is encoded in the triple representation by placing a in the `arg₁` field and (4) in the `arg₂` field.

A ternary operation like `x[i] = y` requires two entries in the triple structure; for example, we can put x and i in one triple and y in the next. Similarly, `x = y[i]` can be implemented by treating it as if it were the two instructions `t = y[i]` and `x = t`, where `t` is a compiler-generated temporary. Note that the temporary `t` does not actually appear in a triple, since temporary values are referred to by their position in the triple structure.

![](img/a29d16e454785bb105e96ef448ac07f6_372_0.png)

|   | op | arg₁ | arg₂ |
|---|---|---|---|
| 0 | `minus` | `c` |  |
| 1 | `*` | `b` | (0) |
| 2 | `minus` | `c` |  |
| 3 | `*` | `b` | (2) |
| 4 | `+` | (1) | (3) |
| 5 | `=` | `a` | (4) |
|   | … |  |  |

(a) Syntax tree

(b) Triples

Figure 6.11: Representations of `a = b * -c + b * -c;`

### Why Do We Need Copy Instructions?

A simple algorithm for translating expressions generates copy instructions for assignments, as in Fig. 6.10(a), where we copy `t₅` into a rather than assigning `t₂ + t₄` to a directly. Each subexpression typically gets its own, new temporary to hold its result, and only when the assignment operator `=` is processed do we learn where to put the value of the complete expression. A code-optimization pass, perhaps using the DAG of Section 6.1.1 as an intermediate form, can discover that `t₅` can be replaced by a.

A benefit of quadruples over triples can be seen in an optimizing compiler, where instructions are often moved around. With quadruples, if we move an instruction that computes a temporary `t`, then the instructions that use `t` require no change. With triples, the result of an operation is referred to by its position, so moving an instruction may require us to change all references to that result. This problem does not occur with indirect triples, which we consider next.

*Indirect triples* consist of a listing of pointers to triples, rather than a listing of triples themselves. For example, let us use an array *instruction list* to point to triples in the desired order. Then, the triples in Fig. 6.11(b) might be represented as in Fig. 6.12.

| instruction | op | arg₁ | arg₂ |
|---|---|---|---|
| 35 (0) | `minus` | `c` |  |
| 36 (1) | `*` | `b` | (0) |
| 37 (2) | `minus` | `c` |  |
| 38 (3) | `*` | `b` | (2) |
| 39 (4) | `+` | (1) | (3) |
| 40 (5) | `=` | `a` | (4) |
| … | … | … | … |

Figure 6.12: Indirect triples representation of three-address code

With indirect triples, an optimizing compiler can move an instruction by reordering the *instruction list*, without affecting the triples themselves. When implemented in Java, an array of instruction objects is analogous to an indirect triple representation, since Java treats the array elements as references to objects.

## 6.2.4 Static Single-Assignment Form

Static single-assignment form (SSA) is an intermediate representation that facilitates certain code optimizations. Two distinctive aspects distinguish SSA from three-address code. The first is that all assignments in SSA are to variables with distinct names; hence the term *static single-assignment*. Figure 6.13 shows the same intermediate program in three-address code and in static single-assignment form. Note that subscripts distinguish each definition of variables p and q in the SSA representation.

```
p = a + b         p₁ = a + b
q = p - c         q₁ = p₁ - c
p = q * d         p₂ = q₁ * d
p = e - p         p₃ = e - p₂
q = p + q         q₂ = p₃ + q₁
```

(a) Three-address code.    (b) Static single-assignment form.

Figure 6.13: Intermediate program in three-address code and SSA

The same variable may be defined in two different control-flow paths in a program. For example, the source program

```
if ( flag ) x = -1; else x = 1;
y = x * a;
```

has two control-flow paths in which the variable x gets defined. If we use different names for x in the true part and the false part of the conditional statement, then which name should we use in the assignment y = x * a? Here is where the second distinctive aspect of SSA comes into play. SSA uses a notational convention called the ϕ-function to combine the two definitions of x:

```
if ( flag ) x₁ = -1; else x₂ = 1;
x₃ = ϕ(x₁, x₂);
```
