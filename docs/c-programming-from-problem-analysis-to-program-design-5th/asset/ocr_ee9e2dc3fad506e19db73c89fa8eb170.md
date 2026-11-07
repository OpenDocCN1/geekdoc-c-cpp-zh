**NOTE** Because these operations are common to all containers, when discussing a specific container, to save space, these operations will not be listed again.

# Member Functions Common to Sequence Containers

The previous section described the member functions that are common to all containers. In addition to these member functions, Table H-6 describes the member functions that are common to all sequence containers, that is, containers of type vector, deque, and list. The name of the function is shown in bold. (Suppose that seqCont is a sequence container.)

**TABLE H-6** Member Functions Common to All Sequence Containers

| Expression | Description |
|---|---|
| `seqCont.insert(position, elem)` | A copy of `elem` is inserted at the position specified by the iterator position. The position of the new element is returned. |
| `seqCont.insert(position, n, elem)` | `n` copies of `elem` are inserted at the position specified by the iterator position. |
| `seqCont.insert(position, beg, end)` | A copy of the elements, starting at `beg` until `end-1`, are inserted into `seqCont` at the position specified by the iterator position. Also, `beg` and `end` are iterators. |
| `seqCont.push_back(elem)` | A copy of `elem` is inserted into `seqCont` at the end. |
| `seqCont.pop_back()` | Deletes the last element. |
| `seqCont.erase(position)` | Deletes the element at the position specified by the iterator position. |
| `seqCont.erase(beg, end)` | Deletes all the elements starting at `beg` until `end-1`. Both `beg` and `end` are iterators. |
| `seqCont.clear()` | Deletes all the elements from the container. |