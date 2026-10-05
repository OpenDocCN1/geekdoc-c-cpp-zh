# 848 Introduction to C++

```
/ If we want to declare iterator variable we'd write
list<int>::iterator it; For simplicity, we use the auto word. */
lst.insert(lst.begin(), arr, arr+5);
cout << "List after insert: ";
for(auto it = lst.begin(); it != lst.end(); ++it)
    cout << *it << ' ';
n
/* We can also use a for-range loop.\nfor(const auto& it : lst)
    cout << it << ' ';\*/

lst.remove(2);
cout << "\nlist after remove: ";
for_each(lst.begin(), lst.end(), show);
lst.unique();
cout << "\nlist after unique: ";
for_each(lst.begin(), lst.end(), show);

lst.pop_front();
lst.push_back(6);
lst.push_back(5);
lst.push_front(7);
lst.sort();
cout << "\nlist after sorting: ";
for_each(lst.begin(), lst.end(), show);

return 0;

void show(int k)
{
    cout << k << ' ';
}
```
```

insert() inserts elements in the position indicated by the iterator. remove() removes all elements that are equal to the argument. unique() removes all duplicate consecutive elements. It keeps only the first element in each group of the same elements. pop_front() removes the first element of the list. push_front() adds the element at the beginning of the list, while push_back() adds it to the end, after its current element. sort() sorts the list. If we use sort() first and then unique() each element appears once. The program uses two ways to display the list, iterator and for_each(). Finally, the program displays:

```
List after insert: 2 2 1 3 1 1
List after remove: 3 1 3 1 1
List after unique: 3 3 1
List after sorting: 1 1 3 5 6 7
```

Note that the non-member sort() we saw earlier requires random access iterators, we can't use it. So, we use the sort() member of the list.

# Container Adaptors

Container adaptors are implemented on top of containers and adapt their functionality to their own requirements. A container adaptor provides a limited set of the services of the encapsulated container, tailored to a specific use. For example, the stack container, although is based on deque,