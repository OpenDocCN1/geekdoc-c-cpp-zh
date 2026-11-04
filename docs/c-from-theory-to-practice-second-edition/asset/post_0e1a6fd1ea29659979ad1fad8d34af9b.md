
type time, and the function should return that structure. Write a program that reads an integer, calls the function, and displays the members of the returned structure.

```c
#include <stdio.h>

struct time
{
    int hours;
    int mins;
    int secs;
};

struct time mk_time(int *ptr);

int main(void)
{
    int secs;
    struct time t;

    printf("Enter seconds: ");
    scanf("%d", &secs);

    t = mk_time(&secs);
    printf("%d:%d:%d\n", t.hours, t.mins, t.secs);
    return 0;
}
```

```c
struct time mk_time(int *ptr)
{
    struct time tmp;

    tmp.hours = *ptr/3600;
    tmp.mins = (*ptr%3600)/60;
    tmp.secs = *ptr%60;
    return tmp;
}
```

Comments: As said, when you want to save time and space, do not return an entire structure. This exercise is just an example to show you how to return a structure. For example, we could change the return type to void and pass the address of t to mk_time(). Thus, the function modifies a structure of the calling function instead of declaring and returning a new structure.

```c
void mk_time(int *ptr, struct time *tmp)
{
    tmp->hours = *ptr/3600;
    tmp->mins = (*ptr%3600)/60;
    tmp->secs = *ptr%60;
}
```

## C.13.5 Define the structure type book with members: title, code, and price. Write a function that takes as parameters two pointers to structures of type book and return the structure with the higher price. Examine the case of the same prices and write a
related message. Write a program that reads and stores the data of 10 books into an array of structures. Then, the program should read two numbers in [1,10] that represent two structure indexes in the array. The program should check the validity of the input numbers and use the function to display the data of the structure with the higher price.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define SIZE 10

struct book
{
    char title[50];
    int code;
    float prc;
};

struct book max_prc(struct book *b1, struct book *b2);
int read_text(char str[], int size, int flag);

int main(void)
{
    int i, j;
    struct book tmp, b[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        printf("\nEnter title: ");
        read_text(b[i].title, sizeof(b[i].title), 1);
        printf("Enter code: ");
        scanf("%d", &b[i].code);
        printf("Enter price: ");
        scanf("%f", &b[i].prc);
        getchar();
    }
    do
    {
        printf("Enter two book numbers [1-%d]: ", SIZE);
        scanf("%d%d", &i, &j);
    } while((i == j) || i > SIZE || j > SIZE || i < 1 || j < 1);
    i--; /* Subtract 1 since indexing starts from 0. */
    j--;
    tmp = max_prc(&b[i], &b[j]);
    if(tmp.prc != 0)
        printf("\nN: %s C: %d P: %.2f\n", tmp.title, tmp.code, tmp.prc);
    else
        printf("\nBoth books have the same price: $%.2f\n", b[i].prc);
    return 0;
}
```

```c
struct book max_prc(struct book *b1, struct book *b2)
{
    struct book tmp = {0};
    if(b1->prc > b2->prc)
        return *b1;
    else if(b1->prc < b2->prc)
        return *b2;
    else
        return tmp;
}
```

## C.13.6 Define the structure type product with members: name, code, and price. Write a function that takes as parameters an array of such structures, the number of the products and a product code. The function should check if a product's code is equal to that number, and if so, it should return a pointer to the respective structure, otherwise NULL. Write a program that uses the type product to read the data of 100 products. The program should store the products that cost more than $20 in an array of such structures. Then, the program should read an integer and use the function to display the product's name and price, if found.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define SIZE 100

struct product
{
    char name[50];
    int code;
    float prc;
};

struct product *find_prod(struct product prod[], int num_prods, int code); /* Declare a function that takes as parameters an array of structures and two integers and returns a pointer to a structure of type product. */
int read_text(char str[], int size, int flag);

int main(void)
{
    int i, cnt, code;
    float prc;
    struct product *ptr, prod[SIZE];
    cnt = 0;
    for(i = 0; i < SIZE; i++)
```

rectangle's diagonal. Each endpoint should be a structure of type coord. The function should calculate and return the area of the rectangle. Write a program that uses the type rectangle to read the coordinates of a rectangle's diagonal and uses the function to display its area.

```c
#include <stdio.h>

struct coord
{
    double x;
    double y;
};

struct rectangle
{
    struct coord point_A; /* First diagonal point. */
    struct coord point_B; /* Second diagonal point. */
};

double rect_area(struct coord *c1, struct coord *c2);

int main(void)
{
    struct rectangle rect;

    printf("Enter the x and y coords of the first point: ");
    scanf("%lf%lf", &rect.point_A.x, &rect.point_A.y);

    printf("Enter the x and y coords of the second point: ");
    scanf("%lf%lf", &rect.point_B.x, &rect.point_B.y);

    printf("Area: %f\n",
        rect_area(&rect.point_A, &rect.point_B));
    return 0;
}

double rect_area(struct coord *c1, struct coord *c2)
{
    double base, height;

    if(c1->x > c2->x)
        base = c1->x - c2->x;
    else
        base = c2->x - c1->x;

    if(c1->y > c2->y)
        height = c1->y - c2->y;
    else
        height = c2->y - c1->y;

    return base*height; /* Return the area. */
}
```

## C.13.8
For a complex number z, we have z = a + bj, where j is the imaginary unit, a is the real part, and b is the imaginary part. Define the structure type complex with members the float numbers re and im, which represent the real and imaginary parts of a complex number. Write a function that takes as parameters two structures of type complex and a character, which represents the sign of a math operation. The function should perform the math operation and return the result as a structure of type complex. Write a program that uses the structure complex to read two complex numbers and a math sign (+, -, *, /) and uses the function to display the result of the math operation. Remind that if z1 = a + bj and z2 = c + dj, we have:

z = z1 + z2 = (a + c) + (b + d)j

z = z1 - z2 = (a - c) + (b - d)j

z = z1 × z2 = (ac - bd) + (bc + ad)j

z = (z1 / z2) = ((ac + bd)/(c² + d²)) + ((bc - ad)/(c² + d²))j

```c
#include <stdio.h>

struct complex
{
    double re; /* The real part of the complex number. */
    double im; /* The imaginary part of the complex number. */
};

struct complex operation(struct complex a1, struct complex a2, char sign);

int main(void)
{
    char sign;
    struct complex z1, z2, z;

    printf("Enter real and imaginary part of the first complex number: ");
    scanf("%lf%lf", &z1.re, &z1.im);
    printf("z1 = %f+%fj\n", z1.re, z1.im);

    printf("Enter real and imaginary part of the second complex number: ");
    scanf("%lf%lf", &z2.re, &z2.im);
    printf("z2 = %f+%fj\n", z2.re, z2.im);

    printf("Enter sign (+, -, *, /): ");
    scanf(" %c", &sign); /* We add a space before %c to skip the new line character stored in stdin. */
    if(sign == '+' || sign == '-' || sign == '*' || sign == '/')
{
    if(sign == '/' && z2.re == 0 && z2.im == 0)
        printf("Division by zero is not allowed\n");
    else
    {
        z = operation(z1, z2, sign);
        printf("z = z1 %c z2 = %f+%fi\n", sign, z.re, z.im);
    }
}
else
    printf("Wrong sign\n");
return 0;
}
```

```c
struct complex operation(struct complex a1, struct complex a2, char sign)
{
    double div;
    struct complex a;
    switch(sign)
    {
        case '+':
            a.re = a1.re + a2.re;
            a.im = a1.im + a2.im;
            break;
        case '-':
            a.re = a1.re - a2.re;
            a.im = a1.im - a2.im;
            break;
        case '*':
            a.re = (a1.re*a2.re) - (a1.im*a2.im);
            a.im = (a1.im*a2.re) + (a1.re*a2.im);
            break;
        case '/':
            div = (a2.re*a2.re) + (a2.im*a2.im);
            a.re = ((a1.re*a2.re) + (a1.im*a2.im))/div;
            a.im = ((a1.im*a2.re) - (a1.re*a2.im))/div;
            break;
    }
    return a;
}
```

Comments: Notice that we're using the flag + in printf() to display the imaginary part of the complex number. Recall from Chapter 2 that the flag + prefixes the positive values with +. The reason we didn't pass the addresses of the structures to operation() is to show you an example of a function with parameters structures.

## C.13.9 Define the structure type student with members: name, code, and grade. Write a program that uses this type to read the data of 100 students and store them in an array of such structures. If the user enters -1 for grade, the insertion of data should terminate. Write a function to sort the structures in grade ascending order and another function to
