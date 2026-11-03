The following example illustrates one possible approach:

```
```c
typedef struct node {struct node *n[]; char color[];} NODE;
typedef NODE *NODE_REF;
typedef union {NODE nd; NODE_REF link;} EXTNODE;
static EXTNODE *next_avail;
make_avail(int num) /* make space available for num NODEs */
{
 int k;
 EXTNODE *p1, *p2;
 next_avail = p1 = calloc(num, sizeof(EXTNODE));
 for (k = 1; k < num; ++k)
 {
 p2 = p1 + 1;
 p1 -> link = p2;
 p1 = p2;
 }
 p1 -> link = NULL;
 /* next_avail points to linked list of num NODEs */
}
new(NODE_REF *ndr) /* get new NODE pointed at by ndr */
{
 *ndr = next_avail;
 if (next_avail != NULL)
 next_avail = next_avail -> link;
}
free(NODE_REF *ndr) /* *ndr rejoins available pool */
{
 ndr -> link = next_avail;
 next_avail = ndr;
 /* *ndr = NULL; /* really free it ! */
}
```
```

If the above constitutes a separate program file, then all access to the dynamic pool of NODES is through calls to make_avail, new, and free. The type names NODE and NODE_REF are, of course, more globally known.

# 6.4 String input-output

Two functions, gets and puts, are provided to allow input and output of an entire array of characters. These functions have virtual declarations:

```
```c
int gets(int fd; char line[]; int max_size);
int puts(int fd; char string[]; int size);
```
```