# Iterator Operations

**Figure 15.9** shows operations that can be performed on each iterator type. In addition to the operators shown for all iterators, iterators must provide default constructors, copy constructors and copy assignment operators. A *forward* iterator supports `++` and all of the *input* and *output* iterator capabilities. A *bidirectional* iterator supports `--` and all the capabilities of *forward* iterators. A *random-access* iterator supports all of the operations shown in the table. For input iterators and output iterators, it’s not possible to save the iterator, then use the saved value later.

**Fig. 15.9 Iterator operations for each type of iterator.**

| Iterator operation | Description |
|---|---|
| *All iterators* | |
| `++p` | Preincrement an iterator. |
| `p++` | Postincrement an iterator. |
| `p = p1` | Assign one iterator to another. |
| *Input iterators* | |
| `*p` | Dereference an iterator as an rvalue. |
| `p->m` | Use the iterator to read the element `m`. |
| `p ==` | Compare iterators for equality. |