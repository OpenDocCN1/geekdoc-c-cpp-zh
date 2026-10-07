# 384

# ABSTRACT DATA STRUCTURES

```
return iter;
}
else{
    std::cout << "Key not found!" << std::endl;
    return end();
}
else{
    std::cout << "Duplicate key!" << std::endl;
    return end();
}
```

For the most part this repeats the theme of this section in that the LTC class insert mimics that for our previous LinkedList apart from some modifications to incorporate template parameters and the replacement of pointers to Node objects with iterators. A slight alteration has been made in that, upon completion of the insertion operation, the LTC insert method returns an iterator that points to the spot of insertion.

Now let us return to the other iterator: const_iterator. As the name suggests, this class provides iterators that can be used for read-only access to LTC objects. To appreciate the need for this type of iterator consider the nonoperative implementation below of the LTC class constructor.

```
template <class Key, class Data> LTC<Key, Data>::LTC(const LTC<Key, Data>& L){
if(L.Size == 0){
    Head = 0;
    Size = 0;
}else{
    Size = L.Size;
    iterator iter;
    Node<Key, Data>* temp = 0;
    for(iter iter = L.begin(); iter != L.end(); iter++){
        if(temp == 0){
            Head = new Node<Key, Data>(iter->dataValue,
            iter->keyValue);
            temp = Head;
        }else{
            temp->Next = new Node<Key, Data>(iter->dataValue,
            iter->keyValue);
            temp = temp->Next;
        }
    }
    temp->Next = 0;//null pointer as Next for tail node
}
```

The solution is to create another iterator class that can access but not alter nodes. Motivated by the analogous STL concept, the class has been named const_iterator.