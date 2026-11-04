This will produce the following output:

```
Filtering 2
2
Filtering 5
Filtering 7
Filtering 4
4
Filtering 1
Filtering 9
Filtering 5
Filtering 8
8
```

In other words, one MoveNext call on the resulting iterator object can cause multiple such calls to take place on the input sequence, which can be an iterator itself. In the case of a filter, the source is consulted until an object is found that passes the filter.

# IENUMERABLE<T> HAS MANY FACES

The beauty of interfaces is how general-purpose they can be, by limiting the number of promises they make between the implementer and user. The IEnumerable family of interfaces is just like that, stating one should be able to enumerate over a sequence of objects somehow.

What the effects of such an enumeration are, or where the data has to come from, is left unspecified. For example, in a List<T>, the data will be persisted in memory while another implementation of the interface could consult a database on the fly, pulling one object over the wire at a time.

This sometimes makes interfaces two-edged swords: The guarantees provided to the interface's user are often very limited, while providing an immense amount of flexibility to the implementers. Only good documentation can help document how an implementer interpreted the interface with regard to various aspects.

The execution model of iterators can be summarized in a simple statement: Every call to MoveNext on an iterator's enumerator object causes the iterator to run until the next yield statement is encountered. A yield return statement will cause MoveNext to return true, with the Current property set to the specified return value, while reaching the end of the iterator or encountering yield break causes it to return false.

As an exercise, step through the following chain of iterators either using raw brainpower or with help of a debugger, assuming a consumer is iterating over it. Figure 20.5 shows the interactions between the iterators for this example.