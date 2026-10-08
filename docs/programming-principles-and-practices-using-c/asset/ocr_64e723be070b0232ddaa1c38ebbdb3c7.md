| Associative container operations (continued) |
| --- |
| p=c.upper_bound(k) p points to the first element with key greater than k. |
| pair(p1,p2)=c.equal_range(k) (p1:p2) are the elements with key k. |
| r=c.key_comp() r is a copy of the key-comparison object. |
| r=c.value_comp() r is a copy of the mapped_value-comparison object. If a key is not found, c.end() is returned. |

The first iterator of the pair returned by `equal_range` is `lower_bound` and the second is `upper_bound`. You can print the value of all elements with the key "Marian" in a `multimap<string,int>` like this:

```
string k = "Marian";
auto pp = m.equal_range(k);
if (pp.first!=pp.second)
  cout << "elements with value " << k << "\n";
else
  cout << "no element with value " << k << "\n";
for (auto p = pp.first; p!=pp.second; ++p)
  cout << p->second << '\n';
```

We could equivalently have used

```
auto pp = make_pair(m.lower_bound(k),m.upper_bound(k));
```

However, that would take about twice as long to execute. The `equal_range`, `lower_bound`, and `upper_bound` algorithms are also provided for sorted sequences (\S B.5.4). The definition of `pair` is in \S B.6.3.

# ## B.5 Algorithms

There are about 60 standard algorithms defined in `<algorithm>`. They all operate on sequences defined by a pair of iterators (for inputs) or a single iterator (for outputs).

When copying, comparing, etc. two sequences, the first is represented by a pair of iterators `[b:e]` but the second by just a single iterator, `b2`, which is considered the start of a sequence holding sufficient elements for the algorithm, for example, as many elements as the first sequence: `[b2:b2+(e-b)].`

Some algorithms, such as `sort`, require random-access iterators, whereas many, such as `find`, only read their elements in order so that they can make do with a forward iterator.