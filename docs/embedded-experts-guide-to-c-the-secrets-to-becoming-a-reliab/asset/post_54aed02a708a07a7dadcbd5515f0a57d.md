
Other than primitive data types (in C, these are pointers, integer and floating point variables), in memory are stored in organised collections of primitive types known as data structures. The C language only supports three types of data structure: arrays, records (which in C are known as structures or structs) and unions. Using the three types of data structures supported by C as building blocks, it is possible to create many other types of data structure, which include queues, stacks, and lists. These compound types are useful, because they allow the programmer to manage memory and to efficiently implement a number of algorithms which cannot be easily performed using only built-in types.

## Arrays

Arrays are the most basic data structure available in C. An array is a collection of variables of the same type which may be identified by their index. Arrays are always allocated as a continuous region in memory; because of this, arrays may also be accessed efficiently using pointers: the statement array[index] is equivalent to *(array + index), and either form may be used to access any array. This easy and useful relationship between arrays and pointers sometimes results in statements claiming the two types are essentially equivalent – this is untrue despite their compatibility. There are a few occasions where the two cannot be used interchangeably (you cannot assign a new address to an array, for instance). There is also an important distinction between them in terms of memory allocation: whereas a pointer definition allocates only the space needed for the pointer variable itself, an array definition allocates all the space required to store the array.

In practice, most arrays are one-dimensional, i.e. only a single index is required to identify any element; however, multidimensional arrays, where elements are identified through multiple indices, are also supported. In the same way a one-dimensional array can be accessed using pointers, a multi-dimensional array may be accessed using pointers to pointers for a two-dimensional array, or however many layers of indirection are required for higher dimensional arrays. Because arrays are allocated to continuous regions of memory, it is also possible to access a multidimensional array using only a single level of indirection, although doing so is usually impractical and highly unlikely to result in code which is easily understood.

Arrays are well-suited to random access operations; read and write operations take the same amount of time regardless of the location in the array being accessed. However, inserting or removing elements from an array arbitrarily is an expensive operation, because it requires significant rearrangement of other elements; other data structures, albeit ones often built using arrays, are better suited to these operations, and some of these will be covered in this chapter.

## Structures

Records are the second type of data structure available in the C language. These are known simply as structures in C and declared using the struct keyword. Structures are used to store variables, referred to as members, intended to be used together; they encapsulate data so it can be treated as a single entity, and in this sense can be viewed as a primitive precursor to classes present in other programming languages. Unlike the elements in an array, the members of a structure are named, rather than indexed, and need not all share the same type. Any type can be used as a structure member, including arrays, other structures, and unions. Structures can be thought of as a means of creating custom, compound types, although, because C does not support operator overloading, there are limits to the ability of the programmer to fully integrate these new types into the language – the assignment operator can be used for the entire structure, rather than individual members, provided the source variable is a compatible structure, but most other operators cannot.

It is also important to remember that struct forms part of the type name (the other part of the name being the tag, which is not strictly required in all cases). This is why typedef is often used in conjunction with structure definitions, although this practice is sometimes frowned upon.

```c
/* Define a custom type using a struct.
 * The new type is “struct fruit_type_s”, not
 * “fruit_type_s”. */
struct fruit_type_s
{
int16_t fruit_id;
char fruit_name[32];
}
/* Give the new type a more straightforward
 * name. We can now declare instances of the
 * type as “fruit_type_t” rather than
 * “struct fruit_type_s”. */
typedef struct fruit_type_s fruit_type_t;
```

Fig 3.1 - A custom struct type can be given a new name using typedef. This allows the type to be used without requiring the struct prefix every time an instance is declared.

## Unions

Unions are used to allocate multiple variables to the same address. A union definition resembles a structure definition, except the keyword union is used instead of struct. Like structures, the name can also include a tag and they have named members, but unlike structures, the members are not independent of each other: they overlap in memory. The members of a union are always of different types; although this is not strictly a requirement of the language, there is little point in using a union to store two variables of the same type. The most common use of unions is for converting a variable from one type to another while preserving the binary representation of the original type. Thus, unions are one method of bypassing the type system in C; they should be considered type-unsafe and used with care. An acceptable use of unions is to pack and unpack individual bytes for use with a serial interface. A pointer to a union is also, in effect, a pointer to each of the members of the union, although an appropriate cast will be required to access the members correctly.

## Linked lists

A linked list is a data structure intended to be accessible sequentially without relying upon the order of elements within memory. To achieve this, each element contains a link to the next element, usually in the form of a pointer. This allows elements to be efficiently inserted to or removed from the list. However, unlike arrays, accessing arbitrary elements within a linked list is not efficient since this can only be achieved by working through the list one element at a time until the required entry is found.

Many variants of the basic linked list exist, which include doubly-linked lists, which may be traversed in either direction (a second link is added to the previous element in the list to allow this), and circular linked lists, where all are circularly linked such that traversing the list will eventually lead back to the element originally accessed. Some variants, such as unrolled linked lists and skip lists, attempt to improve performance either in terms of memory usage or non-sequential access times, albeit at the expense of increased complexity of the implementation.

```c
/* Create a statically allocated list. Each node
 * contains a block of data and a pointer to the
 * next node. */
typedef struct list_node_s
{
struct list_node_s *p_next;
char node_data[LIST_BLOCK_SIZE];
} list_node_t;
static list_node_t list[LIST_NODES];
/* There are actually two lists - we need to keep
 * track of the nodes that haven't been
 * allocated yet. So create pointers to the list
 * head and the free list head. */
static list_node_t *p_list_head;
static list_node_t *p_free_head;
/* Initialise the lists. This function must be
 * called before the list can be used. Each node
 * is added to the free list and points to the
 * next node. */
static void list_init(void)
{
p_list_head = NULL;
p_free_head = list;
for (int index = 0;
LIST_NODES - 1 > index; --index)
{
list[index].p_next = &list[index + 1];
}
list[LIST_NODES - 1].p_next = NULL;
}
/* Add a node to the list and return a pointer
* to the new node. This function also
* initialises the list the first time it is
* called. */
list_node_t * list_add_node(void)
{
static bool is_ready = false;
list_node_t * p_new_node = NULL;
list_node_t * p_end_node = p_list_head;
/* Initialise the list on first call. */
if (!is_ready)
{
list_init();
is_ready = true;
}

/* If there is a free node, add it to the list
* and update the last node to point to
* it. */
if (NULL != p_free_head)
{
/* Find the next free node. */
```
