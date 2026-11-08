Some algorithms have received more general variants of these functions with C++23 and ranges in the `<ranges>` header in the `std::ranges::` namespace and are summarized as *fold operations*. They all start with `fold_` in their names. In the following list, you will see a reference to the more specific function in the corresponding description of the *fold* function. For example, `fold_left` is a more general version of `accumulate`. The remaining classical algorithms can be mapped using range adapters and are thus found in the `std::views::` namespace.

In the overview, I write `std::` before the function names when it is a classical algorithm from the header `<numeric>`, and `rs::` for the new functions from `<ranges>`. In the text, for the sake of clarity, I prefix the range adapters with `vs::`.

+   - **`std::accumulate`**  
+     Usage: constant; iterators: in  
+     This function is suitable for calculating `r = init # a # b # c # ...`. Here, `#` is any binary function or `operator+` if you do not specify one. `init` represents the “neutral” element with respect to the operation (for example, 0 for addition or 1 for multiplication). Subexpressions are always evaluated from left to right, so you must use `reduce` for parallel execution. You can see an example in Listing 25.15.

+   - **`std::reduce`**  
+     Usage: constant; iterators: in  
+     Like `accumulate`, except the grouping is not specified. Therefore, use only associative operators like addition and multiplication. Subtraction, for example, is not associative. Due to this property, `reduce` is particularly suitable for `execution::par`; see Listing 25.4.  
+     Do not underestimate this function. You might have heard of it in another context, perhaps from “MapReduce” or *fold*, *aggregate*, or *compress* from functional languages.

+   - **`rs::fold_left`, `rs::fold_left_first`**  
+     Usage: frequent (C++23); iterators: in  
+     Like `accumulate`, but you always specify the binary operation. The `__first` variants take the first value of the range as the initial value. For the variants without `__first`, you additionally provide the initial value. You get the result of the computation back.

+   - **`rs::fold_left_with_iter`, `rs::fold_left_first_with_iter`**  
+     Usage: occasional (C++23); iterators: in  
+     Like `fold_left` and `fold_left_first`, but returns an iterator.

+   - **`std::adjacent_difference`**  
+     Usage: occasional; iterators: in  
+     This outputs the results of the operations `a#b`, `b#c`, `c#...` etc. into an output container. If you do not provide a binary operator, `operator-` is used. You get a kind of 'discrete derivative' of the values in the container. The output container must have space for `n-1` elements; see Listing 25.16. For ranges, since C++23, use `vs::adjacent_transform`.