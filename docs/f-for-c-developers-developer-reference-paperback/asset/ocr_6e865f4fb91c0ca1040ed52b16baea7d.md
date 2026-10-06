The F# list might suggest it has some relationship with the List<T> type. Actually, the list type is a Microsoft.FSharp.Collections.FSharpList<T> type. It implements the Iumerable<T> interface, and it is not very similar to the List<T> type.

# Sequences

According to MSD documentation, a sequence is a logical series of elements of one type. Sequences are particularly useful when you have a large, ordered collection of data but not necessarily to use all the elements. Individual sequence elements are computed only as required, so a sequence can provide better performance than a list in situations where not all of the elements are needed. Any type that implements the System.IEnumerable interface can be used as a sequence. Defining a sequence is similar to defining a list. Listing 1-25 shows few examples of how to define a sequence.

LISTING 1-25 Defining a sequence in F#

```
// defines a sequence with elements from 1 to 10.
let seq0 = { 1..10 }

// defines a sequence with elements 0, 1, 4, 9, and 16.
let seq2 = { for i=0 to 4 do yield i*i }

// defines a sequence using for..in
let seq1 = {
for i in [1..10] do i * 2
}

// defines an empty sequence
let emptySeq = Seq.empty
```

> Note Be aware that seq { 1; 2; 3 } is not a valid way to define a sequence. However, you can use the yield keyword to define a sequence as shown here: seq { yield 1; yield 2; yield 3 }.

A sequence is shown as an IEnumerable<T> type viewed in C#. When you expose a sequence to a C# project, you do not need to add Microsoft.FSharp.Core.dll.

# Arrays

The definition from MSDN says that arrays are fixed-size, zero-based, mutable collections of consecutive data elements that are all of the same type. Listing 1-26 shows how to define an array.