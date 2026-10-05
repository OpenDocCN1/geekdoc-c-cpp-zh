# 13 • Structures and Unions 397

```
cout << "Enter favourite book: ";
getline(pers_arr[i].d.w.book, sizeof(pers_arr[i].d.w.book);

}
for(i = 0; i < SIZE; i++)
{
    if(pers_arr[i].type == 0)
    {
        cout << "\nGame: " << pers_arr[i].d.m.game << '\n';
        cout << "\nShow: " << pers_arr[i].d.m.movie << '\n';
    }
    else if(pers_arr[i].type == 1)
    {
        cout << "\nMovie: " << pers_arr[i].d.w.tv_show << '\n';
        cout << "Book: " << pers_arr[i].d.w.book << '\n';
    }
}
return 0;
```

The program reads the sex type and stores the user's preferences in the respective union members. To know which of structure, is Man or Woman, is contained in each Person member type is added. In the second loop, the program checks its value and displays the respective preferences.

> It is the programmer's responsibility to keep track which member of the union contains a meaningful value. A special member may be added (like the type above) to indicate what is currently stored in the union.

Another application of unions is to provide multiple views of the same data in order to use the most convenient. For example, in embedded applications, it is often needed to view a register in different ways. How we can use a 32-bit register value in bit field or as a mask:

```
struct Bit_Val
{
    unsigned int CF : 1;
    unsigned int PF : 1;
    /* more bit fields. */
}
```

```
union Flags_Reg
{
    unsigned int i_val;
    Bit_Val b_val;
}
```

Changing the value of i_val alters the values of the bit fields and vice versa. If you ever get involved with such applications, don't forget that the order the bit fields are allocated may differ from system.

Unions are often used in the development of communication protocols for the encoding of the exchanged messages. The following exercise is a simple example on how I used a union when developing a protocol for ISDN networks. If you ever get involved with that field, it might be useful.