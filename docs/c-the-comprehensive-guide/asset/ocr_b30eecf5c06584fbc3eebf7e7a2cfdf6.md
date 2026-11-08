+   - **views::join**  
+     Usage: frequent; iterators: in  
+     Turns a range-of-ranges into a flattened range.
+   
+   - **views::join_with**  
+     Usage: frequent (C++23), iterators: in  
+     Like `ranges::join_view`, but with a separator element between the joined ranges.
+   
+   - **views::split**  
+     Usage: frequent; iterators: fw  
+     A `forward_range` is split into multiple ranges at a delimiter.
+   
+   - **views::lazy_split**  
+     Usage: rare; iterators: in  
+     Also splits, but only requires an `input_range`.
+   
+   - **views::reverse**  
+     Usage: frequent; iterators: in  
+     Reverses a range.
+   
+   - **views::enumerate**  
+     Usage: frequent (C++23); iterators: in  
+     Turns a range of elements into a new range of tuples, each containing an index and the element.
+   
+   - **views::elements**  
+     Usage: occasional; iterators: in  
+     Turns a range of tuples into a range of the *n*-th elements.
+   
+   - **views::keys**  
+     Usage: occasional; iterators: in  
+     Like elements for the first tuple element.
+   
+   - **views::values**  
+     Usage: occasional; iterators: in  
+     Like elements for the second tuple element.
+   
+   - **views::zip**  
+     Usage: constant (C++23); iterators: in  
+     Takes multiple *n* ranges and creates a range of tuples with *n* elements each.
+   
+   - **views::zip_transform**  
+     Usage: frequent (C++23); iterators: in  
+     Like zip, but then calls a function with *n* arguments.
+   
+   - **views::chunk**  
+     Usage: frequent (C++23); iterators: in  
+     Splits a range into multiple ranges of length *n*, without overlap.
+   
+   - **views::chunk_by**  
+     Usage: frequent (C++23); iterators: in  
+     Groups consecutive elements based on a criterion. Reminiscent of SQL's group by.