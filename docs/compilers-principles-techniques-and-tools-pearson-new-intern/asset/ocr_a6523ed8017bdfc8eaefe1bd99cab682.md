# ### 6.3. TYPES AND DECLARATIONS

When type expressions are represented by graphs, two types are *structurally equivalent* if and only if one of the following conditions is true:

+   * They are the same basic type.
+   * They are formed by applying the same constructor to structurally equiva-lent types.
+   * One is a type name that denotes the other.

If type names are treated as standing for themselves, then the first two condi-tions in the above definition lead to *name equivalence* of type expressions. Name-equivalent expressions are assigned the same value number, if we use Algorithm 6.3. Structural equivalence can be tested using the unification algo-rithm in Section 6.5.5.

# ### 6.3.3 Declarations

We shall study types and declarations using a simplified grammar that declares just one name at a time; declarations with lists of names can be handled as discussed in Example 5.10. The grammar is

```
```
D -> T id ; D | ε
T -> B C | record '{' D '}'
B -> int | float
C -> ε | [ num ] C
```
```

The fragment of the above grammar that deals with basic and array types was used to illustrate inherited attributes in Section 5.3.2. The difference in this section is that we consider storage layout as well as types.

Nonterminal *D* generates a sequence of declarations. Nonterminal *T* gen-erates basic, array, or record types. Nonterminal *B* generates one of the basic types **int** and **float**. Nonterminal *C*, for “component,” generates strings of zero or more integers, each integer surrounded by brackets. An array type con-sists of a basic type specified by *B*, followed by array components specified by nonterminal *C*. A record type (the second production for *T*) is a sequence of declarations for the fields of the record, all surrounded by curly braces.

# ### 6.3.4 Storage Layout for Local Names

From the type of a name, we can determine the amount of storage that will be needed for the name at run time. At compile time, we can use these amounts to assign each name a relative address. The type and relative address are saved in the symbol-table entry for the name. Data of varying length, such as strings, or data whose size cannot be determined until run time, such as dynamic arrays, is handled by reserving a known fixed amount of storage for a pointer to the data. Run-time storage management is discussed in Chapter 7.