```
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