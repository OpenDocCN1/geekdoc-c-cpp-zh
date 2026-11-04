```
struct person pers_arr[SIZE];

for(i = 0; i < SIZE; i++)
{
    printf("\nSelection: 0 for man - 1 for woman: ");
    scanf("%d", &type);

    pers_arr[i].type = type;
    getchar();
    if(type == MAN)
    {
        printf("Enter favourite game: ");
        read_text(pers_arr[i].d.m.game, sizeof(pers_arr[i].d.m.game), 1);
        printf("Enter favourite movie: ");
        read_text(pers_arr[i].d.m.movie, sizeof(pers_arr[i].d.m.movie), 1);
    }
    else if(type == WOMAN)
    {
        printf("Enter favourite TV show: ");
        read_text(pers_arr[i].d.w.tv_show, sizeof(pers_arr[i].d.w.tv_show), 1);
        printf("Enter favourite book: ");
        read_text(pers_arr[i].d.w.book, sizeof(pers_arr[i].d.w.book), 1);
    }
}
for(i = 0; i < SIZE; i++)
{
    if(pers_arr[i].type == MAN)
    {
        printf("\nGame: %s\n", pers_arr[i].d.m.game);
        printf("Show: %s\n", pers_arr[i].d.m.movie);
    }
    else if(pers_arr[i].type == WOMAN)
    {
        printf("\nMovie: %s\n", pers_arr[i].d.w.tv_show);
        printf("Book: %s\n", pers_arr[i].d.w.book);
    }
}
return 0;
```

The program reads the sex type and stores the user's preferences in the respective union members. To know which type of structure, that is, man or woman, is contained in each person we added the member type. In the second loop, the program checks its value and displays the respective preferences.

![](bbox=[0.08, 0.92, 0.13, 0.97])

It is the programmer's responsibility to keep track which member of the union contains a meaningful value. A special member may be added (like the type previously) to indicate what is currently stored in the union.