# ISO/IEC 14882:2017(E)

+   (2.1) - T shall be MoveConstructible (Table 23).

+   (2.2) - All of

+   (2.2.1) - binary_op(init, init),
(2.2.2) - binary_op(init, binary_op2(*first1, *first2),
(2.2.3) - binary_op(binary_op2(*first1, *first2), init), and
(2.2.4) - binary_op(binary_op2(*first1, *first2), binary_op2(*first1, *first2))
shall be convertible to T.

+   (2.3) - Neither unary_op nor binary_op should invalidate subranges, or modify elements in the ranges [first1, last] and [first2, first2] + (last - first1)).

+   3 Returns:
GENERALIZED_SUM(binary_op, init, binary_op2(*i, *first2 + (i - first1)), ...)
for every iterator i in [first, last].

+   4 Complexity: O(last - first) applications of binary_op and binary_op2.
template<class InputIterator, class T>
class BinaryOperation, class UnaryOperation>
transform<InputIterator first, InputIterator last, T init,
BinaryOperation op, UnaryOperation up);
template<class ExecutionPolicy, class T>
class ForwardIterator, class BinaryOperation
&& exec
transform_reduce(ExecutionPolicy& exec, ForwardIterator first,
ForwardIterator last, T init, BinaryOperation_op, UnaryOperation_up);

+   5 Requires:
(5.1) - T shall be MoveConstructible (Table 23).

+   (5.2) - All of
(5.2.1) - binary_op(init, init),
(5.2.2) - binary_op(init, unary_op(*first)),
(5.2.3) - binary_op(unary_op(*first), init), and
(5.2.4) - binary_op(unary_op(*first), unary_op(*first))
shall be convertible to T.

+   (5.3) - Neither unary_op nor binary_op should invalidate subranges, or modify elements in the ranges [first1, last].

+   6 Returns:
GENERALIZED_SUM(binary_op, init, unary_op(*i), ...)
for every iterator i in [first, last].

+   7 Complexity: O(last - first) applications of each unary_op and binary_op.

> [Note: transform_reduce does not apply unary_op to init. — end note]