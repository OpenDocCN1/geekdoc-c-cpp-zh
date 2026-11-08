book_author is the member of the structure, which in turn is a structure of type author. To access the first_name member of book_author use

```
    cprog.book_author.first_name
```

Similarly,

```
    cprog.book_author.no_of_pages
```

This value can be incremented by writing

```
    ++cprog.book_author.first_name
```

The first member title is a character array. The fourth element of this array, can be access by using

```
    cprog.title[3]
```

Structure members can be processed in the same manner as ordinary variables of the same data type. Single-valued structure members can appear in expressions, they can be passed to functions, and they can be returned from functions, as though they were ordinary single-valued variables. Complex structure members are processed in the same way as ordinary data items of that same type.

What does this imply? Structure members which are arrays can be processed in the same manner as an ordinary array. Structure member that is a structure can be processed on member at a time in the same manner as any other structure. These operations are shown below

Consider the structure

```
    struct author {
        char first_name[15];
        char last_name[15];
    };
    struct book {
        char title[20];
        struct author book_author;
        int no_of_pages;
        float cost;
    } cprog;
```

Several operations to access structure members

```
    cprog.no_of_pages=455;
```

This statement assigns the value of 455 to cprog.no_of_pages

```
    printf("Book title is %s", cprog.title);
```

This statement passes the array cprog.title to the printf function, so that it could be printed on console.

```
    printf("Author's name %s %s", cprog.book_author.first_name, cprog.book_author.last_name);
```

This statement passes two arrays cprog.book_author.first_name and cprog.book_author.last_name to the printf function, both of which are submembers of structure cprog, so that it could be printed on console.