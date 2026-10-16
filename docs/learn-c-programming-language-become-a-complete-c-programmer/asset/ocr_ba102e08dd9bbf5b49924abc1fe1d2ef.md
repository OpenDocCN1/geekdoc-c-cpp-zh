Sort enough of [b:e) to copy the first e2–b2 elements into [b2:e2), using f for comparison; p is the smaller of b2 and b2+(e–b)
Is [b:e) sorted?
Is [b:e) sorted, using f for comparison?
p points to the first element in [b:e) that is not in order

p=is_sorted_until(b,e,f) p points to the first element in [b:e) that is not in order, using f for comparison

nth_element(b,n,e) *n is in the position it would be in if [b:e) was sorted; elements in [b:n) are <= *n and *n <= elements in [n:e)

nth_element(b,n,e,f) *n is in the position it would be in if [b:e) was sorted; elements in [b:n) are <= *n and *n <= elements in [n:e), using f for comparison

The sort() algorithms require random-access iterators (§33.1.2).
Despite its name, is_sorted_until() returns an iterator, rather than a bool.
The standard list (§31.3) does not provide random-access iterators, so lists should be sorted

using the specific list operations (§31.4.2) or by copying their elements into a vector, sorting that vector, and then copying the elements back into the list:

```
template<typename List> void sort_list(List& lst) {
vector v {lst.begin(),lst.end()}; sort(v);
copy(v,lst);
}
// initialize from lst
// use container sort(§32.2)
```

The basic sort() is efficient (on average N*log(N)). If a stable sort is required, stable_sort() should be used, that is, an N*log(N)*log(N) algorithm that improves toward N*log(N) when the system has sufficient extra memory. The get_temporary_buffer() function may be used for getting such extra memory (§34.6). The relative order of elements that compare equal is preserved by stable_sort() but not by sort().

Sometimes, only the first elements of a sorted sequence are needed. In that case, it makes sense to sort the sequence only as far as is needed to get the first part in order, that is, a partial sort. The plain partial_sort(b,m,e) algorithms put the elements in the range [b:m) in order. The partial_sort_copy() algorithms produce N elements, where N is the lower of the number of elements in the output sequence and the number of elements in the input sequence. We need to specify both the start and the end of the result sequence because that’s what determines how many elements we need to sort. For example:

```
void f(const vector<Book>& sales) // find the top ten books
{
vector<Book> bestsellers(10);
partial_sort_copy(sales.begin(),sales.end(),
bestsellers.begin(),bestsellers.end(),
[](const Book& b1, const Book& b2) { return b1.copies_sold()>b2.copies_sold(); });
```