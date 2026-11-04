# Source Selection Using a from Clause

Query expressions start by the use of a from clause, which has two tasks. First, it refers to the source that's getting queried, such as an in-memory collection or a reference to an object representing a table in a database. Second, it establishes a name for the items in that source, which is used subsequently to express filters, orderings, and so on. The following is an example:

```
var nums = new List<int> { 1, 2, 3, 4, 5 };
from n in nums ...
```

Observe a few things here. On the second line, I've not assigned the query expression to a variable to emphasize it's an expression. You can use the whole query expression as a parameter to a method, assign it to a variable, or whatever else you're allowed to do with an expression.

Next, the from clause cannot stand by itself; it needs to be followed, as indicated by the ellipsis, with other query operators such as projection or grouping, among others. Those other query operators can refer to n whenever they want to express something for an element in the specified source. (In this case, nums acts as the source.)

Because the range identifier n represents an element in the nums source, it had better have the right type for use in the query expression. This type gets inferred from context, typically leveraging generics. In the preceding example, n will eventually be inferred to be of type int. Figure 19.11 shows the code editor revealing the inferred type of the range variable in our query expression.

![](bbox=[0.07, 0.75, 0.45, 0.85])

FIGURE 19.11 The type of a range variable gets inferred.

# GUESSWORK

In fact, the IntelliSense engine is merely making an informed guess here. The code illustrated here doesn't compile because the query expression isn't complete and there wouldn't be enough information for the compiler to infer the type of n just yet. So to be really precise, you shouldn't believe the compiler gets the type of the element directly from the generic type representing the source (for example, List<int>).

You'll see later in this chapter, when we discuss the translation of various query clauses into method calls, that n gets used as the parameter to lambda expressions used in the various query expression clauses. That's where the compiler infers the type from, based solely on all its method overloading knowledge. For esoteric query providers, the type of the range identifier can even change throughout the entire query expression. Pretend you didn't hear this because in all practical cases the type of the range identifier simply corresponds to the type of elements in the queried data source.