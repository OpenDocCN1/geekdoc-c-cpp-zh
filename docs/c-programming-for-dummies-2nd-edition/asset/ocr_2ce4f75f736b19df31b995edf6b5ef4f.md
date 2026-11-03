Listing 16-4 shows how the declarations take place if you were to use typedef to simplify the structures:

# LISTING 16-4: Using typedef to Define a Structure

```
typedef struct id
{
    char first[20];
    char last[20];
} personal;

typedef struct date
{
    int month;
    int day;
    int year;
} calendar;

struct human
{
    personal name;
    calendar birthday;
};
```

In this listing, the structure id is typedef'd to the name personal. This isn't a variable name; it's a typedef. It's the same as saying, “All references to struct id are now the same as the name personal.”

Likewise, the structure date is typedef'd to calendar. Finally, in the declaration of the structure human, the typedef names are used instead of the more complex structure definitions.

Exercise 16-4: Modify the source code from the project you create in Exercise 14-9 (in Chapter 14) to use typedef, as shown in Listing 16-4. Build and run.

It can be argued that using typedef doesn't make your code any more clear than had you just used good variable names and well-formatted text. For example, I don't use typedef because I don't want to have to remember what I've defined. But you will encounter other code that uses typedef. Don't let it freak you out.

To cast the typedef spell, use this format:

`typedef data_type new_type`