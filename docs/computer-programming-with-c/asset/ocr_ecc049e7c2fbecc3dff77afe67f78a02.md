![](bbox=[0.23, 0.1, 0.83, 0.38])

Figure 9.24: Object b1

```
scanf("%d%s%s%f", &b1.id, b1.title, b1.author, &b1.price);
```

To input the ‘date of publishing’ of object *b1*, we need to actually input the members of the inner structure *Date*. This can be done by using the object *dop* which is created as an object of structure *Date*. However, because the object *dop* is itself embedded inside the object memory of *b1* we input the members *dd*, *mm*, and *yyyy* by using a membership operator as shown:

```
scanf("%d%d%d ", &b1.dop.dd, &b1.dop.mm, &b1.dop.yyyy);
```

The following is the full source code that creates two objects of the structure *Book* and takes the data about each book as input from the user. The code also prints the details of the two *Book* objects in tabular format on the computer screen.

```
#include<stdio.h>
struct Book
{
    int id;
    char title[100];
    char author[100];
    float price;
    struct Date
    {
        int dd;
        int mm;
        int yyyy;
    } dop;
};
void main()
```