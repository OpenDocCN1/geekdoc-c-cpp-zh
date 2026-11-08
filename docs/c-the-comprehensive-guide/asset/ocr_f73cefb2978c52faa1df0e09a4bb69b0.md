Creates a view from an iterator and a sentinel. Some adapters, factories, and algorithms also use this type. Useful: When an algorithm returns a subrange, you can extract the iterators of the range with `auto [beg, end] = ...`.

+   - `views::empty`  
+     Usage: occasional; iterators: –  
+     Creates an empty view with no elements.
+   
+   - `views::single`  
+     Usage: occasional; iterators: –  
+     Produces a view that contains a single element.
+   
+   - `views::iota`  
+     Usage: occasional; iterators: –  
+     For an ascending sequence of values. Corresponds to the iota algorithm.
+   
+   - `views::istream`  
+     Usage: rare; iterators: in  
+     A view created by multiple `operator>>`.
+   
+   - `views::repeat`  
+     Usage: occasional (C++23); iterators: in  
+     Repeats the same value.
+   
+   - `views::filter`  
+     Usage: frequent; iterators: in  
+     Filters out elements from a range that satisfy a predicate. Note that you may only modify the result values if the modified value also satisfies the predicate!
+   
+   - `views::transform`  
+     Usage: frequent; iterators: in  
+     Applies a function to each element.
+   
+   - `views::counted`  
+     Usage: rare; iterators: in  
+     Creates a range from an iterator and a count *n*.
+   
+   - `views::take`  
+     Usage: frequent; iterators: in  
+     Passes only the first *n* elements of a range.
+   
+   - `views::take_while`  
+     Usage: frequent; iterators: in  
+     Passes elements as long as a predicate is true.
+   
+   - `views::drop`  
+     Usage: frequent; iterators: in  
+     Skips the first *n* elements of a range.
+   
+   - `views::drop_while`  
+     Usage: frequent; iterators: in  
+     Skips elements as long as a predicate is true.