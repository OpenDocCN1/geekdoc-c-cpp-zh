following erases the first and second elements—that is, those referred to by `begin()` and `begin() + 1:`

```
scores.erase(scores.begin(), scores.begin() + 2);
```

(Because vector provides random access, operations such as `begin() + 2` are defined for the vector class iterators.) If it1 and it2 are two iterators, the STL literature uses the notation [p1, p2) to indicate a range starting with p1 and going up to, but not including, p2. Thus, the range [begin(), end()) encompasses the entire contents of a collection (see Figure 16.3). Also the range [p1, p1) is empty. (The [) notation is not part of C++, so it doesn’t appear in code; it just appears in documentation.)

![](bbox=[0.175, 0.317, 0.706, 0.511])

Figure 16.3 The STL range concept.

> **Note**
> A range [it1, it2) is specified by two iterators it1 and it2, and it runs from it1 up to, but not including, it2.

An `insert()` method complements `erase()`. It takes three iterator arguments. The first gives the position ahead of which new elements are to be inserted. The second and third iterator parameters define the range to be inserted. This range typically is part of another container object. For example, the following code inserts all but the first element of the new_v vector ahead of the first element of the old_v vector:

```
vector<int> old_v;
vector<int> new_v;
...
old_v.insert(old_v.begin(), new_v.begin() + 1, new_v.end());
```

Incidentally, this is a case where having a past-the-end element is handy because it makes it simple to append something to the end of a vector. In this code the new material is inserted ahead of old_v.end(), meaning it’s placed after the last element in the vector:

```
old_v.insert(old_v.end(), new_v.begin() + 1, new_v.end());
```