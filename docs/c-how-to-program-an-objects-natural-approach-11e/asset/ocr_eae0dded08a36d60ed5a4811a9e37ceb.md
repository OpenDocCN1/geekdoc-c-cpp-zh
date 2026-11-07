| Container | Iterator type | Container | Iterator type |
|---|---|---|---|
| Unordered associative containers |  | Container adaptors |  |
| `unordered_set` | forward | `stack` | none |
| `unordered_multiset` | forward | `queue` | none |
| `unordered_map` | forward | `priority_queue` | none |
| `unordered_multimap` | forward |  |  |

# 13.5.4 Predefined Iterator Type Names

The following table shows the predefined iterator type names found in the standard library container class definitions. Not every iterator type name is defined for every container. **The const iterators are for traversing containers that should not be modified. Reverse iterators** traverse containers in the reverse direction.

| Predefined iterator type name | Direction of ++ | Capability |
|---|---|---|
| `iterator` | forward | read/write |
| `const_iterator` | forward | read |
| `reverse_iterator` | backward | read/write |
| `const_reverse_iterator` | backward | read |

**Operations performed on a `const_iterator` return references to `const` to prevent modifying container elements.** Using `const_iterators` where appropriate is another example of the principle of least privilege.

# 13.5.5 Iterator Operators

The following table shows operators for each iterator type. In addition to the operators shown for all iterators, iterators must provide **default constructors** (forward iterators and higher), **copy constructors and copy assignment operators**. A forward iterator supports ++ and all input and output iterator capabilities. A **bidirectional iterator** supports -- and all the capabilities of forward iterators. **Random-access iterators and contiguous iterators** support all of the operations shown in the table. For input iterators and output iterators, it’s not possible to save the iterator, then use the saved value later.

| Iterator operation | Description |
|---|---|
| **All iterators** |  |
| `++p` | Preincrement an iterator, moving it to the next element. |
| `p++` | Postincrement an iterator, moving it to the next element. |
| `p = p1` | Assign one iterator to another. |