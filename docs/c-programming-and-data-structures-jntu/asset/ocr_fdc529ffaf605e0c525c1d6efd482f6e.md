```
{
    switch (user_choice())
    {
        case 1: insert();
            break;

        case 2: item_delete (&first, &last);
            break;

        case 3: list();
            break;

        case 4: search();
            break;

        case 5: return;
    }
}

/* User selects a particular operation to be performed */
char user_choice (void)
{
    char c;

    /* display the menu of available choices */
    printf ("1. Insert an item\n");
    printf ("2. Delete an item\n");
    printf ("3. Print all items\n");
    printf ("4. Search for an item\n");
    printf ("5. Exit\n");

    do
    {
        printf ("Enter your choice: ");
        c = getchar ();
    } while (c < '1' || c > '5');

    return c;
}
```

# Fig. 15.19 Double linked list program—Part II

```
/* Accept and store an item at an appropriate position in the list */
void insert (void)
{
    struct linked_list *info;
    int n;    /* Used to accept user input */

    while (1)
    {
        info = (struct linked_list *) malloc (sizeof(list_entry));
        if (!info)
```