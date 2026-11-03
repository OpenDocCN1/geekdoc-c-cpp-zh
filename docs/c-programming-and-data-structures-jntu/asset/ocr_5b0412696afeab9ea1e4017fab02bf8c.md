```
}
else
{
  /* if p is not the first item in the list, insert i somewhere middle in the list */
  if (p->previous)
  {
    p->previous->next = i;
    i->next = p;
    i->previous = p->previous;
    p->previous = i;
    return;
  }

  /* i would be the new first item */
  i->next = p;
  i->previous = NULL;
  *first = i;
  return;
}
}
/* i should be the last item */
old->next = i;
i->next = NULL;
i->previous = old;
*last = i;
}
```

# Fig. 15.19 Double linked list program—Part IV

```
/* Delete an item from the list */
void item_delete (struct linked_list *first, struct linked_list *last)
{
  struct linked_list *info;
  int s;

  /* accept the number that the user wants to delete */
  printf ("Enter number to be deleted: ");
  scanf ("%d", &s);

  /* find that number in the list */
  info = find (s);

  /* deletion process only if the item is available in the list */
  if (info)
  {
    /* if the first item of the list is to be deleted */
    if (*first == info)
    {
      *first = info->next;
```