# **TABLE 22-9** Various Ways to Declare a `list` Object

| Statement | Description |
|---|---|
| `list<elementType> listCont;` | Creates the empty list container `listCont`. (The default constructor is invoked.) |
| `list<elementType> listCont(otherList);` | Creates the list container `listCont` and initializes it to the elements of `otherList`. `listCont` and `otherList` are of the same type. |
| `list<elementType> listCont(size);` | Creates the list container `listCont` of size `size`. `listCont` is initialized using the default constructor. |
| `list<elementType> listCont(n, elm);` | Creates the list container `listCont` of size `n`. `listCont` is initialized using `n` copies of the element `elm`. |
| `list<elementType> listCont(beg, end);` | Creates the list container `listCont`. `listCont` is initialized to the elements in the range `[beg, end)`, that is, all of the elements in the range `beg...end-1`. Both `beg` and `end` are iterators. |

Table 22–5 described the operations that are common to all containers. Table 22–6 described the operations that are common to all sequence containers. In addition to these common operations, Table 22–10 describes the operations that are specific to a list container. The name of the function implementing the operation is shown in bold.

In Table 22–10, `listCont` is a container of type list.