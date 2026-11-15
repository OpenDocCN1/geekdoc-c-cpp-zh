```
for (i = 0; i < items.Length; i++)
{
    Console.WriteLine(items[i]);
}
}
```

The difference between a statement and an expression lambda is that the statement lambda has a statement block on the right side of the lambda operator, whereas the expression lambda has only an expression (no return statement or curly braces, for example).

Generally, you would read a lambda operator in an expression lambda in the same way you would read a statement lambda: “goes to.” In addition, “becomes” is sometimes clearer. In cases such as the BubbleSort() call, where the expression lambda specified is a predicate (returns a Boolean), it is frequently clearer to replace the lambda operator with “such that.” This changes the pronunciation of the statement lambda in Listing 12.19 to read “first and second such that first is less than second.” One of the most common places for a predicate to appear is in the call to System.Linq.Enumerable’s Where() function. In cases such as this, neither “such that” nor “goes to” is needed. We would read names.Where(name => name.Contains(“ ”)) as “names where names dot Contains a space,” for example. One pronunciation difference between the lambda operator in statement lambdas and in expression lambdas is that “such that” terminology applies more to expression lambdas than to statement lambdas since the latter tend to be more complex.

The anonymous function does not have any intrinsic type associated with it, although implicit conversion is possible for any delegate type as long as the parameters and return type are compatible. In other words, an anonymous method is no more a ComparisonHandler type than another delegate type such as LessThanHandler. As a result, you cannot use the typeof() operator (see Chapter 17) on an anonymous method, and calling GetType() is possible only after assigning or casting the anonymous method to a delegate variable.

Table 12.1 contains additional lambda expression characteristics.