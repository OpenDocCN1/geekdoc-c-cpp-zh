The exception is the *output iterators*, which require additional properties but do not necessarily bring any of the other categories with them.

| Iterator Category | Provider |
|---|---|
| Contiguous | vector, string, array |
| Random access | deque |
| Bidirectional | list, [multi]set, multiset, [multi]map |
| Forward | forward_list, unordered_[multi]{map|set} |
| Output | ostream, inserter |
| Input | istream |

**Table 24.2** Which containers and streams provide iterators of which category?

There are some distinctions to make between different categories of iterators, as follows:

+   - **All iterators**
+     All iterators can be copied and assigned, meaning you can do `it(other)` and `it = other`. Every iterator also can be incremented with `++`.
+   - **Output iterators**
+     These allow you to assign to their dereferenced element with `*it = ...`.
+   - **Input iterators**
+     These support comparison with `it == ij` and `it != ij` and can return the value of the dereferenced element with `*it` and `it->...`.
+   - **Forward iterators**
+     These are input iterators that in addition guarantee that you can traverse a sequence multiple times if the underlying container does not change. This is the *multipass guarantee*. What that means becomes clear when you consider what happens with iterators that are input iterators but not forward iterators. This is the case, for example, when an iterator reads from `cin`—which changes the state of `cin` upon input and is therefore certainly not multipass capable.
+   - **Bidirectional iterators**
+     These are forward iterators, but can also be decremented with `--it` and `it--`.
+   - **Random access iterators**
+     *Random access iterators* are bidirectional and support addition `+/=` and subtraction `-/=` with integers, as well as comparisons with `>`, `<`, `>=`, and `<=`. The combination of addition and dereferencing also implies that dereferencing with an offset `it[...]` is supported.