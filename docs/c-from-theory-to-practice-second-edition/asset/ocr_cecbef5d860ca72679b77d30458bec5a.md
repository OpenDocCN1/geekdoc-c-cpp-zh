```
struct product /* Since the type date is declared, it can be used to declare nested structures. */
{
    char name[50];
    double price;
    struct date s_date;
    struct date e_date;
};

int main(void)
{
    struct product prod;

    strcpy(prod.name, "product");
    prod.s_date.day = 1;
    prod.s_date.month = 9;
    prod.s_date.year = 2012;

    prod.e_date.day = 1;
    prod.e_date.month = 9;
    prod.e_date.year = 2015;

    prod.price = 7.5;
    printf("The product's life is %d years\n", prod.e_date.year - prod.s_date.year);
    return 0;
}
```

Notice that in order to access a member of the nested structure, the . operator must be used twice. The program subtracts the respective members and displays the product's life.

Let's see a special case. Suppose that we want to declare two mutually dependent structures, the structure A, which contains a structure of type B, and the structure B, which contains a structure of type A. If we write something like:

```
struct A
{
    struct B b;
    ...
};

struct B
{
    struct A a;
    ...
};
```

the compiler will display an error message for the declaration of b because it has no idea about B and its size. If we reverse the declarations, the compiler will display the same type of error for the member a and the unknown structure A. One way to overcome this situation is to make b pointer (we change both for similarity):

```
struct B; /* Incomplete declaration. */
struct A
```