Once we have defined a Date data type, we can create Date variables as follows:

```
// struct4.c
typedef struct {
    int month;
    int day;
    int year;
} Date;
int main(void) {
    Date yesterday, today, tomorrow, appointment, birthday;
    ...
    ...
    return 0;
}
```

# Structure Initialization

Structure initialization is similar to array initialization, except that the data types being initialized may be different for each member. For example:

```
// struct5.c
Date birthday = { 8, 23, 96 };
```

Note that the elements listed inside the brackets are separated by commas. If there are fewer initializers than members, the remaining members are initialized to zero.