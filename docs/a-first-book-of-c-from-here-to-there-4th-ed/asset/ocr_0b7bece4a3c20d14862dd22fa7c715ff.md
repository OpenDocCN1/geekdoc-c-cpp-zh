# Table 13.4 Summary of deque Class Methods and Operations

| Methods and Operations | Type | Description |
|---|---|---|
| deque<DataType> name | constructor | Creates an empty deque named name with a compiler-dependent initial size |
| deque<DataType> name(source) | constructor | Creates a copy of the source deque |
| deque<DataType> name(n) | constructor | Creates a deque of size n |
| deque<DataType> name(n, object) | constructor | Creates a deque of size n with each object initialized as object |
| deque<DataType> name(src.beg, src.end) | constructor | Creates a deque initialized with objects from a source container beginning at src.beg and ending at src.end |
| ~deque<DataType>() | destructor | Destroys the deque and all objects it contains |
| name.at(index) | accessor | Returns the object at index and throws an exception if the index is out of bounds |
| name.front() | accessor | Returns the first object at the front of the deque with no check for the existence of a first object |
| name.pop_front() | mutator | Removes but does not return the first object at the front of the deque |
| name.push_front(object) | mutator | Inserts object at the front of the deque |
| name.back() | accessor | Returns the object at the back of the deque with no check for the existence of a last object |
| name.pop_back() | mutator | Removes but does not return the last object at the back of the deque |
| name.push_back(object) | mutator | Inserts object at the back of the deque |
| name.insert(itr, object) | mutator | Inserts object at iterator position itr |
| name.insert(itr, src.beg, src.end) | mutator | Inserts object at iterator position itr |