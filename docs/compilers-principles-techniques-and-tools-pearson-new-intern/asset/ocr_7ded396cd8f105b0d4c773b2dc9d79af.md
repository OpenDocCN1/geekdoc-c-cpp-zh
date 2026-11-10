# Why Do We Need Copy Instructions?

A simple algorithm for translating expressions generates copy instructions for assignments, as in Fig. 6.10(a), where we copy `t₅` into a rather than assigning `t₂ + t₄` to a directly. Each subexpression typically gets its own, new temporary to hold its result, and only when the assignment operator `=` is processed do we learn where to put the value of the complete expression. A code-optimization pass, perhaps using the DAG of Section 6.1.1 as an intermediate form, can discover that `t₅` can be replaced by a.

![](bbox=[0.286, 0.369, 0.474, 0.484])

|   | op | arg₁ | arg₂ |
|---:|:---|:---|:---|
| 0 | minus | c | |
| 1 | * | b | (0) |
| 2 | minus | c | |
| 3 | * | b | (2) |
| 4 | + | (1) | (3) |
| 5 | = | a | (4) |
|   | … | | |

(a) Syntax tree

(b) Triples

Figure 6.11: Representations of `a = b * -c + b * -c;`

`t = y[i]` and `x = t`, where `t` is a compiler-generated temporary. Note that the temporary `t` does not actually appear in a triple, since temporary values are referred to by their position in the triple structure.

A benefit of quadruples over triples can be seen in an optimizing compiler, where instructions are often moved around. With quadruples, if we move an instruction that computes a temporary `t`, then the instructions that use `t` require no change. With triples, the result of an operation is referred to by its position, so moving an instruction may require us to change all references to that result. This problem does not occur with indirect triples, which we consider next.

*Indirect triples* consist of a listing of pointers to triples, rather than a listing of triples themselves. For example, let us use an array *instruction list* to point to triples in the desired order. Then, the triples in Fig. 6.11(b) might be represented as in Fig. 6.12.

With indirect triples, an optimizing compiler can move an instruction by reordering the *instruction list*, without affecting the triples themselves. When implemented in Java, an array of instruction objects is analogous to an indirect triple representation, since Java treats the array elements as references to objects.