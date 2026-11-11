# 9.7  Passing Object as an Argument to a Function

Similar to any other variable, we can also pass the structure variable as an argument to the function. The following is the code that defines a function `display()`, to print the details of each of the Book object passed to it as an argument.

```
```c
#include<stdio.h>
struct Book
{
int id;
char title[100];
char author[100];
float price;
};
void display(Book t)
{
printf("%d\t%s\t%s\t%f\n",t.id,t.title,t.author,t.price);
}
void main()
{
struct Book b1,b2;
printf("Enter id, title, author and price of the first Book\n");
scanf("%d%s%s%f",&b1.id,b1.title,b1.author,&b1.price);
printf("Enter id, title, author and price of the second Book\n");
scanf("%d%s%s%f",&b2.id,b2.title,b2.author,&b2.price);
printf("The Book details are\n");
display(b1);
display(b2);
}
```
```

# Output

```
```text
Enter id, title, author and price of the first Book
1 C++ Kunal 900
Enter id, title, author and price of the second Book
2 Java Jack 800
The Book details are
1       C++     Kunal   900.000000
2       Java    Jack    800.000000
```
```

The statement,

```
```c
display(b1);
```
```

invokes a function display() by passing the object b1 as an argument to it. Thus, the actual argument b1 is initialized to a formal argument t as shown in Figure 9.30. Hence the members of object b1 can be accessed by using object t in the display() function. The statement: