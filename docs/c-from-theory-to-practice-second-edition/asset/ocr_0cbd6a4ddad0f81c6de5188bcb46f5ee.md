For example, suppose that N = 5 and the keys are 7, 23, 10, 43, 84, 90, and 60. The keys would be stored in the array like this:

+   - [0] :10 ->90 ->60 ->NULL
+   - [1] :NULL
+   - [2] :7 ->NULL
+   - [3] :23 ->43 ->NULL
+   - [4] :84 ->NULL

In position [0], a linked list of three nodes is created. To explain, each key k is examined. If k % 5 equals 0, a node with key value equal to k is created. As a result, three nodes are created with keys 10, 90, and 60, respectively. In position [1] no list is created because there is no key k so that k % 5 equals 1. The remaining positions are configured in the same way.

To search for a key k, we use the hash function to get the position and start searching from that point. For example, suppose that we want to check if the key 53 is stored in the array. The position to look for is 53 % 5 = 3. Next, we traverse the linked list in position [3], to see if the key is stored.

The following program provides an implementation example of the insert and search functions. The array used for storing the keys is an array of pointers.

```
#include <stdio.h>
#include <stdlib.h>

#define SIZE 5

typedef struct node
{
    int key;
    struct node *next;
} node;

int hash_func(int key);
void insert_key(node **cur, int key);
node* find_key(node *p, int key);
void free_mem(node *hash_arr[]);

int main(void)
{
    node *p, *hash_arr[SIZE] = {NULL};
    int i, pos, key;
    for(i = 0; i < 10; i++) /* Insert 10 keys. */
    {
        printf("Enter key: ");
        scanf("%d", &key);
        pos = hash_func(key);
        insert_key(&hash_arr[pos], key);
    }
    printf("Enter key to search: ");
    scanf("%d", &key);
    pos = hash_func(key);
```