# Member Functions Common to Sequence Containers

The previous section described the member functions that are common to all containers. In addition to these member functions, Table 21-6 describes the member functions that are common to all sequence containers, that is, containers of type vector, deque, and list. The name of the function is shown in bold. (Suppose that seqCont is a sequence container.)

**TABLE 21-6 — Member Functions Common to All Sequence Containers**

| Expression | Description |
|---|---|
| `seqCont.insert(position, elem)` | A copy of `elem` is inserted at the position specified by the iterator `position`. The position of the new element is returned. |
| `seqCont.insert(position, n, elem)` | `n` copies of `elem` are inserted at the position specified by the iterator `position`. |
| `seqCont.insert(position, beg, end)` | A copy of the elements, starting at `beg` until `end-1`, is inserted into `seqCont` at the position specified by the iterator `position`. Also, `beg` and `end` are iterators. |
| `seqCont.push_back(elem)` | A copy of `elem` is inserted into `seqCont` at the end. |
| `seqCont.pop_back()` | Deletes the last element. |
| `seqCont.erase(position)` | Deletes the element at the position specified by the iterator position. |
| `seqCont.erase(beg, end)` | Deletes all of the elements starting at `beg` until `end-1`. Both `beg` and `end` are iterators. |
| `seqCont.clear()` | Deletes all of the elements from the container. |
| `seqCont.resize(num)` | Changes the number of elements to `num`. If `size()` grows, the new elements are created by their default constructor. |
| `seqCont.resize(num, elem)` | Changes the number of elements to `num`. If `size()` grows, the new elements are copies of `elem`. |