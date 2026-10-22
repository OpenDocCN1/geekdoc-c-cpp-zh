As you’d expect, fold expressions are pack expansions. Note that if the pack is empty, the type of the fold expression can still be determined from the non-pack operand (value in the forms above).

However, the designers of this feature also wanted an option to leave out the value operand. Two other forms are therefore available in C++17: The unary right fold

```
(pack op ... ) and the unary left fold
(... op pack) Again, the parentheses are required. Clearly this creates a problem for empty expansions: How do we determine their type and value? The answer is that an empty expansion of a unary fold is generally an error, with three exceptions: • An empty expansion of a unary fold of && produces the value true,.
```

+   - An empty expansion of a unary fold of || produces the value false.
+   - An empty expansion of a unary fold of the comma operator (,) produces a void expression.

Note that this will create surprises if you overload one of these special operators in a somewhat unusual way. For example: Click here to view code image

```
struct BooleanSymbol {
...;
};

BooleanSymbol operator||(BooleanSymbol, BooleanSymbol);

template<typename... BTs> void symbolic(BTs... ps) {
BooleanSymbol result = (ps || ...);
...
}
```

Suppose we call symbolic with types that are derived from BooleanSymbol. For all expansions, the result will produce a BooleanSymbol value except for the empty expansion, which will produce a bool value.¹² We therefore generally caution against the use of unary fold expressions, and recommend using binary fold expressions instead (with an explicitly specified empty expansion value).

# 12.5 Friends

The basic idea of friend declarations is a simple one: Identify classes or functions that have a privileged connection with the class in which the friend declaration appears. Matters are somewhat complicated, however, by two facts: