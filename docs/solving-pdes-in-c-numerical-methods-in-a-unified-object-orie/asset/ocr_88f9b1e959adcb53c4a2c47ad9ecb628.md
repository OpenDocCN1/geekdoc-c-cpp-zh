The first field in the "linkedList" object, "item", needs no explicit command to destroy it, because it is not a pointer. It is destroyed automatically right after "next" is destroyed.

Further, we define recursive functions that return a reference to the last item in the linked list and the number of items in it. These functions are then used to append a new item at the end of the linked list:

```
linkedList& last(){
    return next ? next->last() : *this;
} // last item
```

```
int length() const{
    return next ? next->length() + 1 : 1;
} // number of items
```

```
void append(T&t){
    last().next = new linkedList(t);
} // append item
```

The following functions insert new items at different locations in the linked list. The function "insertNextItem()" places the new item right after the first item in the linked list:

```
void insertNextItem(T&t) {
    next = new linkedList(t,next);
} // insert item in second place
```

The function "insertFirstItem()" places the new item just before the first item in the linked list:

```
void insertFirstItem(T&t){
    next = new linkedList(item,next);
    item = t;
} // insert item at the beginning
```

Finally, we also declare some more functions, including functions that drop certain items from certain places in the linked list. (The full definition of these functions will be given later.)

```
void dropNextItem();
void dropFirstItem();
const linkedList& operator+=(linkedList&);
linkedList& order(int);
template<class S>
    const S truncateItems(double, const S&);
template<class S>
    const S dropPositiveItems(
        int, const S&, double);
template<class S>
    const S maskItems(
        const dynamicVector<int>&, const S&);
};
```