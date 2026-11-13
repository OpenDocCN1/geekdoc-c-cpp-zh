# Hash Table Program in C

Hash Table is a data structure which stores data in an associative manner. In hash table, the data is stored in an array format where each data value has its own unique index value. Access of data becomes very fast, if we know the index of the desired data.

# Implementation in C

```
#include <stdio.h> #include <string.h> #include <stdlib.h> #include <stdbool.h>
#define SIZE 20
struct DataItem { int data;
int key;
};
struct DataItem* hashArray[SIZE]; struct DataItem* dummyItem; struct DataItem* item;
int hashCode(int key){ return key % SIZE; }
struct DataItem *search(int key) {//get the hash
int hashIndex = hashCode(key);
//move in array until an empty while(hashArray[hashIndex] != NULL){
if(hashArray[hashIndex]->key == key) return hashArray[hashIndex]; //go to next cell
++hashIndex;
//wrap around the table hashIndex %= SIZE; }
return NULL; }
void insert(int key,int data){
struct DataItem *item = (struct DataItem*) malloc(sizeof(struct DataItem)); item->data = data;
item->key = key;
//get the hash
int hashIndex = hashCode(key);
//move in array until an empty or deleted cell
while(hashArray[hashIndex] != NULL && hashArray[hashIndex]->key != -1) {//go to next cell
++hashIndex;
//wrap around the table hashIndex %= SIZE; }
hashArray[hashIndex] = item; }
struct DataItem* delete(struct DataItem* item) { int key = item->key;
//get the hash
int hashIndex = hashCode(key);//move in array until an empty
while(hashArray[hashIndex] != NULL){
```