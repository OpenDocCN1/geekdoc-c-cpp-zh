# Chapter 15: Collection Interfaces with Standard Query Operators

| Program | Enumerable | Console | IEnumerable<Patent> | Enumerable<Patent> | Enumerator |
| --- | --- | --- | --- | --- | --- |
| Main | Where-Patent | | | | |
| | WriteLine | 1 | | | |
| | GetEnumerator() | | | | |
| | Current() | | | | |
| | MoveNext() | | | | List Display Triggered for Item |
| | WriteLine | 2 | | | |
| | Count-Patent() | List Display Triggered | | | |
| | WriteLine | 3 | | | |
| | ToArray-Patent() | List Display Triggered | | | |
| | Write | | | | | |
| | Count-Patent() | List NOT Triggered | | | |
| | WriteLine | | | | |

15.2: Sequence of operations invoking lambda expressions

Second, a call to Enumerable.Count() (the function) triggers the lambda expression for each item once more. Again, it is subtle because Count (the property) is very common on collections that have not been queried with a standard query operator.

Third, the call to ToArray() (or ToList(), ToDictionary(), or ToLookup()) evaluates the lambda expression for each item. However, converting the collection on which the standard query operator has already executed. In Listing 15.14, the conversion to an array that means when Length is called in the final Console.WriteLine(), the underlying object pointed to by patents is, in fact, an array (which obviously implements IEnumerable<T>); in turn, System.Array's implementation of Length is called rather than System.Linq.Enumerable's implementation.


.System.Linq.Enumerable's implementation. Consequently, following a conversion to one of the collection types returned by a “To” method, it is generally safe to work with the collection (until another standard query operator is called). However, be aware that this will bring the entire result set into memory (it may have been backed by a database or file prior to this step). Furthermore, the “To” method will take a snapshot of the underlying data, so that no fresh results will be returned upon requerying the “To” method result.