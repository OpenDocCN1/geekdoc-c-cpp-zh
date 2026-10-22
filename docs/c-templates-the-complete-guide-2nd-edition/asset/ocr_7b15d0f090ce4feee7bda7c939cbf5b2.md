```
Stack<int>  intStack1, intStack2;  // stacks for ints
Stack<float> floatStack;          // stack for floats
...
intStack1 = intStack2;            // OK: stacks have same type
floatStack = intStack1;           // ERROR: stacks have different types
```