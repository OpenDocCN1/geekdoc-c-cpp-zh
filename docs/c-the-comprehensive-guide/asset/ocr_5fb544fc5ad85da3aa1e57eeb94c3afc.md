```
for(int idx = 0; idx < 100; ++idx)
    v.push_back(idx);
// ...
}
```

**Listing 24.30** Typically, you append at the end in vector.

`emplace_back` takes the same arguments as the constructor of the element you want to append. The container ensures that the new object is created in place and does not need to be copied again. Here, for example, it is the string literal `"Lincoln"` that benefits from using `emplace_back` (and potentially) needs to be copied one less time than if you wrote the following:

```
presidents.push_back(President{"Heuss", 1949});
```

# Deleting from a “vector”

There is `erase` as a method for *all* containers except array, and in `forward_list` there is `erase_after`. In vector, you can either pass an iterator to remove a single element or a pair to remove an entire range:

+   - **All elements**
+     `clear()` removes all elements from the vector. Its size is then zero.
+   - **Last element**
+     `pop_back()` is the best method to remove a single element from a vector. It is the counterpart to `push_back`. It takes O(1).
+   - **Single arbitrary element**
+     `iterator erase(const_iterator where)` deletes a single element. All elements with a larger position than the deleted one are shifted (or copied) one position to the left to fill the gap. This takes O(n) time for a vector and should therefore not be done repeatedly.
+   - **Range**
+     `iterator erase(const_iterator from, const_iterator to)` deletes all elements between from and to, exclusive of to—mathematically noted as a half-open interval `[from..to)`. For clarification, `erase(begin(), end())` is equivalent to `clear()`. Here too elements shift left to fill the gap. This takes O(n) time for a vector.

After the delete operation, the vector is smaller by one element or by the distance between the two iterators.

The return value is an iterator pointing to the first shifted element.

> **Only Container Methods Actually Delete**
> 
> As a rule of thumb: Only methods like `erase` actually delete elements from a container, thus changing its size. Free functions like remove from `<algorithm>` do not delete, but