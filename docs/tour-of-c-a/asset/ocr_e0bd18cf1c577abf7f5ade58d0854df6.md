scheduler will decide how much concurrency to use. This is all nontrivial and the rule against making statements about efficiency without measurement is very important here.

Unfortunately, the range of the parallel algorithms are not yet in the standard, but if we need them, they are easy to define:

Click here to view code image

```
void sort(auto pol, random_access_range auto& r)
{
  sort(pol.begin(),r.end());
}
```

Most standard-library algorithms, including all in the table in §13.5 except equal_range, can be requested to be parallelized and vectorized using par and par unseq for sort. Why not equal_range()? So far nobody has come up with a worthwhile parallel algorithm for that. Many parallel algorithms are used for numeric data; see §17.3.1. When requesting parallel execution, be sure whether it could be expressed as data races (§18.2) and deadlock (§18.3).

# 13.7 Advice

+   [1] An STL algorithm operates on one or more sequences; §13.1.
[2] An input sequence is half-open and defined by a pair of iterators; §13.1.
[3] You can define your own iterators to serve special needs; §13.1.
[4] Many algorithms can be applied to I/O streams; §13.3.1.
[5] When searching, an algorithm usually returns the end of the input sequence to indicate “not found"; §13.2.
[6] Algorithms do not directly add or subtract elements from their argument sequences; §13.2; §13.5.
[7] When writing a loop, consider whether it could be expressed as a general algorithm; §13.2.
[8] Use using-type-aliases to clean up messy notation; §13.2.
[9] Use predicates and other function objects to give standard algorithms a wider range of meanings; §13.4, §13.5.
[10] A predicate must not modify its argument; §13.4.
[11] Know your standard-library algorithms and prefer them to hand-crafted loops; §13.5.