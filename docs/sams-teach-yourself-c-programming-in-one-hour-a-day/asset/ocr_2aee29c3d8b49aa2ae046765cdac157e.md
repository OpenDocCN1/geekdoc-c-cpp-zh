```
43:    printf("nMust be a to z: \");
44:    ch = getc(stdin);      /* get next char in buffer */
45:    gets(trash);               /* remove trash from buffer */
46:    } while (ch < 'a' || ch > 'z') && (ch < 'A' || ch > 'Z'));
47:
48:
49:    first = add_to_list( ch, first );
50:
51:    show_list( first );       /* Dumps the entry list *\n52:    free_memory_list( first );   /* Release all memory */
53:    return 0;
54: }
55:
56: /*/===================================================================*/
57:    * Function: add_to_list() Inserts new link in the list
58:    * Purpose : int ch = character to store
59:    * Entry : int ch LISTPTR first = address of head pointer
60:    * Returns : Address of head pointer (first)
61: /*/==================================================================*/
62:
63: LISTPTR add_to_list( int ch, LISTPTR first )
64:
65: {
66:    LISTPTR new_rec = NULL;      /* Holds address of new rec */
67:    LISTPTR tmp_rec = NULL;     /* Holds tmp pointer */
68:    LISTPTR prev_rec = NULL;
69:
70:    /* Allocate memory. */
71:    new_rec = (LISTPTR)malloc(sizeof(LIST));
72:    if (!new_rec)               /* Unable to allocate memory */
73:    {
74:        printf("\nUnable to allocate memory!\n");
75:        exit(1);
76:    }
77:
78:    /* set new link's data */
79:    new_rec->ch = ch;
80:    new_rec->next_rec = NULL;
81:
82:    if (first == NULL)          /* adding first link to list */
83:    {
84:        first = new_rec;
85:        new_rec->next_rec = NULL;   /* redundant safe * */
86:    }
87:    else                        /* not first record * */
88:    {
89:        /* see if it goes before the first link * */
90:        if (new_rec->next_rec < first->ch)
91:        {
92:            new_rec->next_rec = first;
93:            first = new_rec;
```