In Fig. 11.3, a hash table with Max = 10, both keys 322 and 262 probe to address 2. A chain, a linked list, stores all items at a particular home address (home address is an address within the hash table itself).

![](bbox=[0.313, 0.183, 0.796, 0.396])

Fig. 11.3 An example of chaining

Let us compare rehashing and chaining (Table 11.16).

Table 11.16 Comparison of chaining and rehashing

| Chaining | Rehashing |
|---|---|
| Unlimited number of synonyms can be handled. | A limited but good number of synonyms are taken care of. |
| Additional cost to be paid is an overhead of multiple linked lists. | The table size is doubled but no additional fields of links are to be maintained. |
| Sequential search through the chain takes more time. | Searching is faster when compared to chaining. |

Program Code 11.3 illustrates chaining.

```
PROGRAM CODE 11.3
#define MAX 10
class node
{
 public:
  int key;
  struct node *next;
};
Node *hashtable[max];
```