The discussed increment and decrement operators can also be applied to properties and indexers if both getters and setters are available:

```
vector["x"]--;
person.Age++;
```

# Summary

In this chapter, we explored one of the key sources of expressiveness in the C# programming language developers can live without: expressions. After covering the role of expressions and the runtime’s evaluation stack, we covered one particular set of expressions; namely, operators.

The discussion of operators brought you to arithmetic operators and aspects of overflow checking using the checked and unchecked keywords. Use of floating-point arithmetic was explained as well, focusing on implications of limited precision. Next, you looked at other kinds of operators, such as relation and logical ones. The conditional operator (commonly referred to as the ternary operator) was covered too, pointing out its lazy evaluation of operands. You also learned various aspects of working with null and nullable value types, including the null-coalescing operator.

Finally, you learned various forms of assignment, ranging from simple to compound. This also allowed you to learn increment and decrement operators, as commonly seen in for loops to update an index variable.

Chapter 6, “A Primer on Types and Objects,” focuses on the concept of types from an expression angle. More specifically, you learn how you can check for types, create new object instances, access members on objects, and so on.