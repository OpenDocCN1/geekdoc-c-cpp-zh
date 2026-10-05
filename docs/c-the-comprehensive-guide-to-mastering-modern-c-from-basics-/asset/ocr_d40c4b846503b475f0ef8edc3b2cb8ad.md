In Figure 20.1, you can see how this looks in memory.

| ... | |
|---|---|
| Oxaafe | |
| Oxab00 | |
| Oxab02 | pValue | Oxab04 |
| Oxab04 | value | 42 |
| Oxab08 | |
| Oxab0a | |
| Oxab0c | |
| ... | |

**Figure 20.1** You can think of memory locations as houses on a street.

The definition of pValue in the second line requires an explanation. Because pValue is not an int, int* pValue = value; would be incorrect; you do not need the value from value, but its *address*. And this is exactly what the unary address operator & before the variable name does: &value gives you the address of value. Because value is of type int, &value is of type int*. The assignment of &value to int* pValue is therefore correct.