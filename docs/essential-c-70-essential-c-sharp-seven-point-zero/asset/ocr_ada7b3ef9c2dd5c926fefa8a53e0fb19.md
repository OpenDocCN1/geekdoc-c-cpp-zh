# **OUTPUT 16.7**

```
Keywords:
abstract as base bool break byte case catch char checked class
const continue decimal default delegate do double else enum
event explicit extern false finally fixed float for foreach goto if
implicit in int interface internal is lock long namespace new null
operator out override object params private protected public
readonly ref return sbyte sealed short sizeof stackalloc static
string struct switch this throw true try typeof uint ulong unsafe
ushort using virtual unchecked void volatile while
Contextual Keywords:
add alias ascending async await by descending dynamic equals from
get global group into join let nameof on orderby partial remove
select set value var where yield
```

The group clause results in a query that produces a collection of IGrouping<TKey, TElement> objects—just as the GroupBy() standard query operator did (see Chapter 15). The select clause in the subsequent query uses a tuple to effectively rename IGrouping<TKey, TElement>.Key to IsContextualKeyword and to name the subcollection property Items. With this change, the nested foreach loop uses wordGroup.Items rather than wordGroup directly, as shown in Listing 16.10. Another potential item to add to the tuple would be a count of the items within the sub-collection. This functionality is already available through LINQ’s wordGroup.Items.Count() method, however, so the benefit of adding it to the anonymous type directly is questionable.

# **Query Continuation with into**

As we saw in Listing 16.11, you can use an existing query as the input to a second query. However, it is not necessary to write an entirely new query expression when you want to use the results of one query as the input to another. You can extend any query with a **query continuation** clause using the contextual keyword *into*. A query continuation is nothing more than syntactic sugar for creating two queries and using the first as the input to the second. The range variable introduced by the *into* clause (groups in Listing 16.11) becomes the range variable for the remainder of the query; any previous range variables are logically a part of the earlier query and cannot be used in the query continuation. Listing 16.12 shows how to rewrite the code of Listing 16.11 to use a query continuation instead of two queries.