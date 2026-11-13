# Delete Operation

Whenever an element is to be deleted, compute the hash code of the key passed and locate the index using that hash code as an index in the array. Use linear probing to get the element ahead if an element is not found at the computed hash code. When found, store a dummy item there to keep the performance of the hash table intact.

```
struct DataItem* delete(struct DataItem* item){ int key = item->key;

//get the hash
int hashIndex = hashCode(key);

//move in array until an empty while(hashArray[hashIndex] !=NULL){
if(hashArray[hashIndex]->key == key){
struct DataItem* temp = hashArray[hashIndex];

//assign a dummy item at deleted position hashArray[hashIndex] = dummyItem; return temp;
}
//go to next cell
++hashIndex;

//wrap around the table
hashIndex %= SIZE;
}
return NULL;
}
```

To know about hash implementation in C programming language, please click here.