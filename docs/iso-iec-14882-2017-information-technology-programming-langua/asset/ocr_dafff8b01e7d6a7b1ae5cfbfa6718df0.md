# ISO/IEC 14882:2017(E)

```
ForwardIterator first, Size n);
template <class InputIterator, class ForwardIterator>
ForwardIterator uninitialized_copy(InputIterator first, InputIterator last,
ForwardIterator result);
tntemplate <class ExecutionPolicy, class InputIterator, class ForwardIterator>
ForwardIterator uninitialized_copy(ExecutionPolicy&& exec, // see 28.4.3
InputIterator first, InputIterator last,
ForwardIterator result);
template <class InputIterator, class Size, class ForwardIterator>
ForwardIterator uninitialized_move(InputIterator first, Size n,
ForwardIterator result);
template <class ExecutionPolicy, class InputIterator, class Size, class ForwardIterator>
ForwardIterator uninitialized_move(ExecutionPolicy&& exec, // see 28.4.3
InputIterator first, Size n,
ForwardIterator result);
template <class InputIterator, class ForwardIterator>
ForwardIterator uninitialized_move(InputIterator first, InputIterator last,
ForwardIterator result);
template <class ExecutionPolicy, class InputIterator, class Size, class ForwardIterator>
ForwardIterator uninitialized_move(ExecutionPolicy&& exec, // see 28.4.3
InputIterator first, InputIterator last,
ForwardIterator result);
template <class InputIterator, class Size, class ForwardIterator>
pair<InputIterator, ForwardIterator>
uninitialized_move(InputIterator first, Size n, ForwardIterator result);
template <class ExecutionPolicy, class InputIterator, class Size, class ForwardIterator>
uninitialized_move(ExecutionPolicy&& exec, // see 28.4.3
InputIterator first, InputIterator last,
ForwardIterator result);
template <class ExecutionPolicy, class ForwardIterator, class T>
void uninitialized_fill(ExecutionPolicy&& exec, ForwardIterator first, 
const T& x);
template <class ForwardIterator, class Size, class T>
void uninitialized_fill(ForwardIterator first, Size n, const T& x);
ForwardIterator result;
template <class ExecutionPolicy, class ForwardIterator, class Size, class T>
void uninitialized_fill(ExecutionPolicy&& exec, // see 28.4.3
ForwardIterator first, Size n, const T& x);
ForwardIterator result;
template <class T>
void destroy_at(T*);
template <class ForwardIterator>
void destroy(ForwardIterator first, ForwardIterator last);
template <class ExecutionPolicy, class ForwardIterator>
void destroy(ExecutionPolicy&& exec, // see 28.4.3
ForwardIterator first, ForwardIterator result);
template <class ForwardIterator, class Size>
void destroy_n(ForwardIterator first, Size n);
template <class ExecutionPolicy, class ForwardIterator, class Size>
void destroy_n(ExecutionPolicy&& exec, // see 28.4.3
ForwardIterator first, Size n);
```