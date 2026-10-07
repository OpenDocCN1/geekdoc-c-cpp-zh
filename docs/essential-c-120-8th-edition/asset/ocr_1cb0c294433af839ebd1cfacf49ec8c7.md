```
{
  Console.Write(" * " + (wordGroup.Key ? keyword.Replace("*", null) : keyword));
}
//...
```

# Output 16.6

Keywords:
abstract base bool break byte catch char checked class const continue decimal delegate do double else event explicit extern false fixed float foreach if implicit in interface internal is lock namespace new null operator over object private protected public readonly free return sbyte select short size stackalloc static string struct this throw true try typeof uint unsafe ushort using unchecked void volatile while
Contextual Keywords:
add alias async await by descending dynamic equals from get global group join let nameof nonnull onby partial remove select set value where yield

There are several types to note in Listing 16.10. First, the query result is a sequence of elements of type IGrouping<bool, string>. The first type argument indicates that the "group key" expression following was of type bool, and the second type argument indicates that the "group element" expression following group group was of type string. That is, the query produces a sequence of groups where the Boolean key is the same for each string in the group.

Because a query with a group by clause produces a sequence of collections, the common pattern for iterating over the results is to create nested foreach loops. In Listing 16.10, the outer loop iterates over the groupings and prints out the type of keyword as a header. The nested loop prints each keyword in the group as an item below the header.

The result of this query expression is itself a sequence, which you can query like any other sequence. Listing 16.11 and Output 16.7 show how to create an additional query that adds a projection onto onto which produces a sequence of groups. The next section, on query continuations, shows a more pleasant syntax for adding more query clauses to a complete query.)