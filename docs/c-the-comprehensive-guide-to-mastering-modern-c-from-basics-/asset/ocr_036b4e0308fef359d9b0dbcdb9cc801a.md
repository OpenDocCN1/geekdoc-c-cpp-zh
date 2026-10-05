+   - std::adjacent_difference
Usage: occasional; iterators: in
This outputs the results of the operations a#b, b#c, c#
etc into an output container. If you do not provide a binary operator, operator- is used. You get a kind of 'discrete derivative' of the values in the container.
The output container must have space for n-1 elements;
see Listing 25.16. For ranges, since C++23, use
vs::adjacent_transform.

+   - std::inner_product
Usage: occasional; iterators: in
The inner product of two ranges {a,b,c,...} and
{x,y,z,...} is r=a*x + b*y + c*z + ... As always, you can also
choose the default operators + + yourself.
The result is a single 'accumulated' value. The order of
operations is from left to right; for parallel execution,
use transform_reduce.

+   - std::transform_reduce
Usage: rare; iterators: in
First applies a functor to each element before reduce is
executed. Some overloads take two input ranges,
allowing you to link multiple containers, resulting in a
parallel variant of inner_product, as the order is not
specific. Not equivalent, but the C++23
vs::adjacent_transform range adapter and its
vs::pairwise_transform specialization work similarly.

+   - std::partial_sum
Usage: frequent; iterators: in/out
Similar to accumulate, elements are summed sequentially (or combined with an operator you