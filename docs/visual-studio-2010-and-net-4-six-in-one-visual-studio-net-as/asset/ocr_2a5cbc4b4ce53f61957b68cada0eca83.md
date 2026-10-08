# Sequences

All F# collections, such as lists and arrays, implement the System.Collections.IEnumerable<T> interface. In F# code, you often see this interface type as seq<T>, which is a type abbreviation for this interface type. As in .NET code, sequences are lazy data structures. They are enumerated on demand, and sequence values are not computed until they are requested.

It is important to understand that, using sequences, you can turn F# lists and arrays lazy by operating on them with the various Seq.* static members. As you will see, there is a lot of similarity between these and the aggregate operations defined in the List module in Table 25-11, and, indeed, this is true for all F# collections as well. However, the Seq module also supports operations for calculating minimum, average values, sort and average, and traverse in various ways to pick elements.

**TABLE 25-14:** Selected Aggregate Operators from the Seq Module

| FUNCTION | TYPE | DESCRIPTION |
| Seq.append | seq<'T> -> seq<'T> -> seq<'T> | Appends two sequences, keeping the result lazy. |
| Seq.average | seq<'T> -> 'T | Computes the average of the elements in the sequence. |
| Seq.cast | IIEnumerable -> seq<'T> | Wraps an untyped collection to a typed sequence. |
| Seq.choose | ('T -> 'U) -> seq<'T> -> seq<'U> | Returns a new sequence whose elements, when applied to the given predicate, return Some. |
| Seq.collect | ('T -> seq<'U>) -> seq<'T> -> seq<'U> | Applies the function to each element, and returns a new sequence with the results concatenated. |
| Seq.concat | seq<'T> -> seq<'T> | Concatenates sequences of sequences into a single sequence. |
| Seq.distinct | 'T -> seq<'T> | Returns all distinct elements. |
| Seq.empty | seq<'T> | Returns an empty sequence. |
| Seq.exists | ('T -> bool) -> seq<'T> -> bool | Tests if any element satisfies the given predicate. |
| Seq.filter | ('T -> bool) -> seq<'T> -> seq<'T> | Filters all elements that satisfy the given predicate. |
| Seq.find | ('T -> bool) -> seq<'T> -> 'T | Finds the first element that satisfies the given predicate. |