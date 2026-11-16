listing knowledge in the form of a table and thus translating the table into computer code by rule induction. An example of an OAV triple table is shown in Table 2.1. Induction is a powerful tool of logic that is often missed. The classic example is asking someone why they haven't backed up their hard drive. The usual faulty inductive answer is that their hard drive has never crashed and so by induction it never will. (Stockbrokers love this kind of "reasoning.") For more details on inductive logic programming, see [Bergadano 96].

OAV triples are especially useful for representing facts and the patterns to match the facts in the antecedent of a rule. The semantic net for such a system consists of nodes for objects, attributes, and values connected by HAS-A and IS-A links. If only a single object is to be represented and inheritance is not required, then an even simpler representation called **attribute-value (AV) pairs** may suffice.

# Table 2.1 An OAV Table

| Object | Attribute | Value |
|---|---|---|
| apple | color | red |
| apple | type | mcintosh |
| apple | quantity | 100 |
| grapes | color | red |
| grapes | type | seedless |
| grapes | quantity | 500 |

# 2.6 PROLOG AND SEMANTIC NETS

Semantic nets are easy to translate into PROLOG. For example, the following PROLOG statements express some of the relationships in the semantic net of Figure 2.5:

```
is_a(goodyear_blimp, blimp).
is_a(spirit_of_st_louis, special).
has_shape(blimp, ellipsoidal).
has_shape(balloon, round).
```

Notice that a period marks the end of a PROLOG statement.

# Essentials of PROLOG

Each of the statements above is a PROLOG **predicate expression**, or simply a predicate, because it is based on predicate logic. However, PROLOG is not a true predicate logic language because it is a computer language with executable statements. In PROLOG a predicate expression consists of the predicate name, such as is_a, followed by zero or more arguments enclosed in parentheses and separated