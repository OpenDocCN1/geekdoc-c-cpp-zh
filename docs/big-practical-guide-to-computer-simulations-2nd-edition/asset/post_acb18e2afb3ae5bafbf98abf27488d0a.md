
![](img/0dfb82b7d27bdfebb8b65cb33de3626a_189_0.png)

Fig. 6.6 How the algorithm solves the 4-queens problem.

early with N [Abramson and Yung (1986); Abramson and Yung (1989); Sosic and Gu (1991)].

## 6.6 Lists

In the previous sections, elementary algorithms were presented. Now we turn to data structures, which are special ways to arrange data in memory such that algorithms can be implemented as efficiently as possible. Note that for different types of tasks, different data structures are most suitable, hence one always has to have the target application in mind. This also explains why a careful planning of the simulation program before actually starting programming is very recommendable, see Chap. 3. Furthermore, note that usually data structures which allow for very fast operations sometimes require some degree of redundancy. Very often, the quicker the operations are, the more memory you have to consume. Hence, efficiency in terms of running time comes at the expense of efficiency in terms of memory, and vice versa.

Assume that you are writing a simulation package for describing the social interactions of persons. For each person, there is always a (sometimes empty) set of other people who are currently interacting with the person. This set may change in time. Hence, we would like to have a data structure to store all current acquaintances in a flexible way, i.e., persons can be easily added and removed from the set. Here, we present a data structure called a list, which allows to solve this task. Lists are, for example, used in atomistic simulation packages for implementing short-range interactions. In this case, for each atom interacts only with atoms not too far away. In this case, for each atom a list is used (a so-called “Verlet table”) to store the atoms which are currently in the neighborhood.⁴ Another example for lists are waiting queues, which consist of tasks given in a linear order, where one task has to be performed after the other. Here, also the order of the elements is important, as for many applications, in contrast to acquaintance lists or the Verlet tables. Note that the example applications and implementations given below are rather simple, in contrast to the real applications just mentioned, to keep the subject as simple as possible.

Lists are generalizations of arrays of elements (of arbitrary type). Lists also exhibit a linear order like arrays, i.e., there is always a first element, for each element there is a successor, except for the last element of the list. For an array, the order of the elements is fixed. If you want to remove, say, the 5th element in an array of 100 elements, and you want to keep the order of the remaining elements, then you have to copy the 6th element to the 5th position, the 7th element to the 6th, and so on, see Fig. 6.7. Hence, for an array of N elements, O(N) operations are needed to remove an element from the list while keeping the order. Also O(N) operations are required when an element is inserted into an array. Furthermore, the size of an array is fixed, hence usually one stores the number of the last element which is used and the maximum number of allowed elements. Now, if the number of elements to be stored grows larger than the number of allowed elements, one has to use realloc to obtain more memory, which might lead to a considerable amount of memory copy operations, if the free amount of memory right behind the array does not provide enough available memory to satisfy the request.

For lists, on the other hand, the size and the order are not fixed. Hence, they are designed in such a way that insert and delete operations can always be performed in constant running time. The most natural implementation for this purpose is using *pointers*, see Sec. 1.4. The basic idea is that each element carries a pointer, which points to its successor. Here, we show a sample C structure, which implements lists, and, for simplicity, just stores integer numbers.

| GET SOURCE CODE |
|---|
| DIR: algorithms |
| FILE(S): list.h |

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_191_0.png)

Fig. 6.7  Removing an element from an array, such that the order of the remaining elements is conserved. Unused array elements are indicated by a line —. The last element used in the array is stored in the variable *last*. Top: array before removing the third element, which contains the number 56 (marked by an X). Bottom: final situation, all elements to the right of the third position have moved one position to the left.

```
struct elem_struct
{
    int                    info;             /* holds "information" */
    struct elem_struct *next;  /* pointer to successor (last: NULL) */
};

typedef struct elem_struct elem_t;           /* new type for nodes */
```

Each element consists of two variables. The actual data is stored in `info`, while the successor in the list is stored in `next`. We have used also a `typedef` command, which allows, for convenience, to refer to the new list data type in the same way as for a predefined data type.

A list is a collection of elements, which are linked in a way such that a linear order is represented, e.g. see Fig. 6.8. Such a list is denoted as *single-linked*, because each element stores one pointer, i.e. link. Lists where each element stores two pointers, one to its successor and one to its predecessor, are also widespread and called *double-linked lists*. Double-linked lists require more memory, due to the additional elements, but some

```
int delete_element(elem_t *elem)
{
    if(elem == NULL)
    {
        fprintf(stderr, "attempt to delete 'nothing'\n");
        return(1);
    }
    else if(elem->next != NULL)
    {
        fprintf(stderr, "attempt to delete linked element!\n");
        return(1);
    }
    else
    {
        free(elem);
        return(0);
    }
}
```

The function contains two consistency checks. First, it is not allowed to delete “nothing” (lines 3-7). Second, it is only allowed to delete isolated elements (lines 8-12), which is indicated by a successor given by a NULL pointer. The actual deletion consists just of the free() command (line 15).

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_193_0.png)

Fig. 6.9 Inserting an element containing an 8 into the list from Fig. 6.8. Either the element is inserted at the beginning (top) or elsewhere into the list (bottom). In both cases the final situation after the insertion is shown.

To assemble lists from elements, we use the insert_element() function, which inserts an element (represented by a pointer elem) into a list (represented by a pointer list to the first element), *after* a given element **where**, which is already member of the list. There are two cases to be considered. Either the new element is inserted at the beginning of the list, in this case **where** contains the NULL pointer. Note that this case applies in particular when the list is empty, hence the new element is used to create a new list. The second case is the general case that **where** points to an existing member of the list. The two cases are illustrated in Fig. 6.9.

The function `insert_element()` receives exactly the three pointers `list`, `elem`, and `where` as arguments. Note that in the case the new element is inserted at the beginning, the pointer to the first element of the list, which represents the list itself and is defined outside `insert_element()`, has to be changed. To allow for this update, the function returns always a pointer to the current first element.

```c
elem_t *insert_element(elem_t *list, elem_t *elem, elem_t *where)
{
    if(where==NULL)                      /* insert at beginning ? */
    {
        elem->next = list;
        list = elem;
    }
    else                                 /* insert elsewhere */
    {
        elem->next = where->next;
        where->next = elem;
    }
    return(list);
}
```

In the case where the element is inserted at the beginning (lines 3–7), one has to change the pointer to the first element and to assign the successor `next` of the inserted element `elem`, as indicated in Fig. 6.9. In the other case (lines 8–12), also the successor of the inserted element is assigned, but also the predecessor is assigned to point to `elem`. Note that many other strategies for building lists are possible. One could, for example, insert elements such that they are ordered according to some criterion. Also, there are some special list types where inserting elements happens always at the beginning (for so-called *stacks*) or at the end (for *waiting queues*). For stacks, elements which arrived last are taken out first, this is called *last-in first-out* (LIFO). For waiting queues, elements which arrived first are taken out first, this is called *first-in first-out* (FIFO). As usual, we refer
