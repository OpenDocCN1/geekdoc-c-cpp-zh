```
const T& getValue() const{
    return item.getValue();
} // read only first-item value

int getColumn() const{
    return item.getColumn();
} // read only first-item column
```

Since the "row" class is derived from the "linkedList" class, it can use its public and protected members. In particular, it can use the functions that insert or drop items. Still, the "row" class contains its own local versions of the "insertNextItem", "insertFirstItem" and "append" functions. These versions are different from the original versions in Chapter 3, Section 5, since they take two arguments to specify the value and the column of the inserted element. The definitions of the present versions call the corresponding original version. In these calls, the prefix "linkedList::" precedes the function name to indicate that an original version is called:

```
void insertNextItem(const T&val, int col){
    rowElement<T> e(val,col);
    linkedList<rowElement<T> >::insertNextItem(e);
} // insert a rowElement as second item

void insertFirstItem(const T&val, int col){
    rowElement<T> e(val,col);
    linkedList<rowElement<T> >::insertFirstItem(e);
} // insert a rowElement at the beginning

void append(const T&val, int col){
    rowElement<T> e(val,col);
    linkedList<rowElement<T> >::append(e);
} // append a rowElement at the end of row
```

The recursive structure of the base "linkedList" class is particularly useful. The definitions of many member functions use recursive calls applied to the "next" field that points to the rest of the row. However, the "next" field inherited from the base "linkedList" class is of type pointer-to-linkedList rather than pointer-to-row. Therefore, it must be converted explicitly to pointer-to-row before the recursive call can take place. This is done by adding the prefix "(row*)".

Usually, this conversion is considered as risky because in theory "next" can point to a "linkedList" object or any object derived from it, with a completely different interpretation of the recursively called function. Fortunately, here "next" must point to a "row" object, so the conversion is safe.

As a matter of fact, this explicit conversion could be avoided by introducing another member function of the form

```
row* nextElements(){
    return (row*) this->next;
} // implicit conversion of the inherited pointer "next"
```