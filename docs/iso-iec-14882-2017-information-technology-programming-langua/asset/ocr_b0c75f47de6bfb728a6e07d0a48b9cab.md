# ISO/IEC 14882:2017(E)

```
template<class BidirectionalIterator, class BidirectionalIterator2>
BidirectionalIterator2 copy_backward(
BidirectionalIterator first, BidirectionalIterator last,
BidirectionalIterator result);
```

```
// 28.6.2. move
template<class InputIterator, class OutputIterator>
OutputIterator move(InputIterator first, InputIterator last,
OutputIterator result);
template<class ExecutionPolicy, class ForwardIterator1,
class ForwardIterator2>
ForwardIterator2(ExecutionPolicy&& exec, // sec 28.4.5
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result);
template<class BidirectionalIterator, class BidirectionalIterator2>
BidirectionalIterator move_backward(
BidirectionalIterator first, BidirectionalIterator last,
BidirectionalIterator result);
```

```
// 28.6.3. swap
template<class ForwardIterator1, class ForwardIterator2>
ForwardIterator2 swap_ranges(ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 first2);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
ForwardIterator2 swap_ranges(ExecutionPolicy&& exec, // sec 28.4.3
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 first2);
template<class ForwardIterator1, class ForwardIterator2>
void it_swap(ForwardIterator1 a, ForwardIterator2 b);
```

```
// 28.6.4. transform
template<class InputIterator, class OutputIterator, class UnaryOperation>
OutputIterator transform(InputIterator first, InputIterator last,
OutputIterator result, UnaryOperation op);
template<class InputIterator, class OutputIterator, class BinaryOperation>
OutputIterator transform(InputIterator first, InputIterator last,
OutputIterator first2, OutputIterator result, BinaryOperation op);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
class UnaryOperation>
ForwardIterator2 transform(ExecutionPolicy&& exec, // sec 28.4.5
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 result, UnaryOperation op);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
class BinaryOperation>
ForwardIterator2 transform(ExecutionPolicy&& exec, // sec 28.4.5
ForwardIterator1 first, ForwardIterator1 last,
ForwardIterator2 first2, ForwardIterator2 result,
BinaryOperation op);
```

```
// 28.6.5. replace
template<class ForwardIterator, class T>
void replace(ForwardIterator first, ForwardIterator last,
const T& old_value, const T& new_value);
```