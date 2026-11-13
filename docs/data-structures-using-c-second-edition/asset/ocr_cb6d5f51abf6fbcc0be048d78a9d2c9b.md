![](bbox=[0.16, 0.1, 0.86, 0.29])

# Operations on a Chained Hash Table

Searching for a value in a chained hash table is as simple as scanning a linked list for an entry with the given key. Insertion operation appends the key to the end of the linked list pointed by the hashed location. Deleting a key requires searching the list and removing the element.

Chained hash tables with linked lists are widely used due to the simplicity of the algorithms to insert, delete, and search a key. The code for these algorithms is exactly the same as that for inserting, deleting, and searching a value in a single linked list that we have already studied in Chapter 6.

While the cost of inserting a key in a chained hash table is O(1), the cost of deleting and searching a value is given as O(n) where n is the number of elements in the list at that location. Searching and deleting takes more time because these operations scan the entries of the selected location for the desired key.

In the worst case, searching a value may take a running time of O(n), where n is the number of key values stored in the chained hash table. This case arises when all the keys are inserted into the linked list of the same location (of the hash table). In this case, the hash table is ineffective.

Table 15.1 gives the code to initialize a hash table as well as the codes to insert, delete and search a value in a chained hash table.

| Struture of the node | Code to insert a value |
| :--- | :--- |
| typedef struct node_HT { int value; struct node *next; }node; | /* The element is inserted at the beginning of the linked list whose pointer to its head is stored in the location given by h(k). The running time of the insert operation is O(1), as the new key value is always added as the first element of the key list irrespective of the size of the linked list as well as that of the chained hash table. */ void *insert_value( node *hash_table[], int val) { node *new_node; new_node = (node *)malloc(sizeof(node)); new_node value = val; new_node next = hash_table[h(x)]; hash_table[h(x)] = new_node; } |
| **Code to initialize a chained hash table** | |
| /* Initializes m location in the chained hash table. The operation takes a running time of O(m) */ void InitializeHashTable (node *hash_table[]); int m) { int j; for(j=0;j<m;j++) hash_table[j]=NULL; } | |