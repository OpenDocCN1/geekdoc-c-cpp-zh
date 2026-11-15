The reason for this is to enable IntelliSense, or the ability to predict the members on the objects being selected. For example, because from appears first and identifies the string array Keywords as the data source, the code editor knows that word is of type string. This enables IntelliSense—member access (a dot operation) on word will display only the members of string. If the from clause appeared after the select, then any dot operations prior to the from clause would not know what the data type of word was, and, therefore, would not be able to display a list of word’s members. In Listing 15.1, for example, it wouldn’t be possible to predict that Contains() was a possible member of word. word is referred to as a range variable; it represents each item in the collection.

# Projection

The output of a query expression is an IEnumerable<T> or IQueryable<T> collection.¹ The data type of T is inferred from the select or groupby clause. In Listing 15.1, for example, the data type of string is inferred from select word because word is a string, word’s data type is the type argument of the IEnumerable<T> collection in the from clause. Since Keywords is a string array, it implements IEnumerable<string>, and therefore, word is a string.

The type resulting from an expression which queries a collection of a certain type is by no means limited to be a sequence of that original type. Rather, the select clause allows for projection of data into an entirely different type. Consider the query expression in Listing 15.2, and its corresponding output in Output 15.2.

```
LISTING 15.2: Projection Using Query Expressions
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;

// ...
```

1. Query expression output is practically always IEnumerable<T>, but theoretically, not necessarily. Nothing is stopping anyone from coming up with an implementation of the query operators that returns something else. To do so would be somewhat perverse, but there is no requirement in the language that query operators return IEnumerable<T>.