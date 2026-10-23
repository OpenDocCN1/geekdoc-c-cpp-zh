```
```cpp
template<class T>
template<class S>
const S linkedList<T>::maskItems(
const dynamicVector<int>& mask, const S&){
S sum=0.;
if(next){
int dropped = 0;
for(linkedList<T>* runner = this;
runner->next;
runner = dropped ? runner : runner->next){
if(!mask[runner->next->item.getColumn()]){
sum += runner->next->item.getValue();
runner->dropNextItem();
dropped = 1;
}
}
}
if(next&&(!mask[item.getColumn()])){
sum += item.getValue();
dropFirstItem();
}
return sum;
} // masking items
```
```

# # 3.8 The Merging Problem

Users to linked lists may want to manipulate them in many ways. For example, they may want to insert items into them or drop items from them. Furthermore, they would like to be able to do this without dealing with storage issues such as pointers and addresses. The functions that perform these tasks are described above.

Users of linked lists may want to do another operation: merge two ordered linked lists with each other while preserving the order. Completing this task efficiently is called the merging problem.

The power of templates is apparent here. Indeed, it is particularly convenient to deal with an unspecified type 'T', provided that it supports some order. This way, we can concentrate on the data structure under consideration rather than the type used in the variables in it. It is only when the merging function is called that the concrete type is specified.

In the following, we describe a function that merges two linked lists into a single linked list while preserving the order. It is assumed that the type 'T' of the items in the linked list supports a complete priority order; that is, every two 'T' objects can be compared by the '<', '>', and "==" binary operators.

This priority order may take all sorts of different interpretations. Indeed, if the '<', '>', and "==" operators of the 'T' class have the usual meaning, then the items in the 'T' class should be ordered in increasing-value order, from the smallest to the largest. If, on the other hand, these operators are interpreted in the 'T' class in terms of absolute value.