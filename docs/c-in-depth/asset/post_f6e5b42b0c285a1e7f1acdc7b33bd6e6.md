
```c
printf("Enter the element : ");
scanf("%d",&m);
printf("Enter the position after which this element is inserted : ");
scanf("%d",&position);
addafter(m,position);
break;
case 4:
if(start==NULL)
{
printf("List is empty\n");
continue;
}
printf("Enter the element for deletion : ");
scanf("%d",&m);
del(m);
break;
case 5:
display();
break;
case 6:
printf("Enter the element to be searched : ");
scanf("%d",&m);
search(m);
break;
case 7:
exit();
default:
printf("Wrong choice\n");
}/*End of switch*/
/*End of while*/
/*End of main()*/

create_list(int data)
{
struct node *q,*tmp;
tmp=malloc(sizeof(struct node));
tmp->info=data;
tmp->link=NULL;
if(start==NULL) /*If list is empty*/
start=tmp;
else
{
/*Element inserted at the end*/
q=start;
while(q->link!=NULL)
q=q->link;
q->link=tmp;
}
}
/*End of create_list()*/
```

```c
addatbeg(int data)
{
struct node *tmp;
tmp=malloc(sizeof(struct node));
tmp->info=data;
tmp->link=start;
start = tmp;
}
/*end of addatbeg()*/
```

```c
addafter(int data, int pos)
{
struct node *tmp, *q;
int i;
q=start;
for(i=0;i<pos-1;i++)
{
    q=q->link;
    if(q==NULL)
    {
        printf("There are less than %d elements", pos);
        return;
    }
}
/*End of for*/
tmp=malloc(sizeof(struct node));
tmp->link=q->link;
tmp->info=data;
q->link=tmp;
}
/*End of addafter()*/
```

```c
del(int data)
{
struct node *tmp,*q;
if(start->info==data)
{
    tmp=start;
    start=start->link; /*First element deleted*/
    free(tmp);
    return;
}
q=start;
while(q->link->link!=NULL)
{
    if(q->link->info==data)/*Element deleted in between*/
    {
        tmp=q->link;
        q->link=tmp->link;
        free(tmp);
        return;
    }
    q=q->link;
}
/*End of while */
if(q->info==data) /*Last element deleted*/
{
    tmp=q->link;
    free(tmp);
    q->link=NULL;
    return;
}
printf("Element %d not found\n",data);
}/*End of del()*/
```

```c
display()
{
    struct node *q;
    if(start==NULL)
    {
        printf("List is empty\n");
        return;
    }
    q=start;
    printf("List is :\n");
    while(q!=NULL)
    {
        printf("%d ",q->info);
        q=q->link;
    }
    printf("\n");
}/*End of display() */
```

```c
search(int data)
{
    struct node *ptr=start;
    int pos=1;
    while(ptr!=NULL)
    {
        if(ptr->info==data)
        {
            printf("Item %d found at position %d\n",data,pos);
            return;
        }
        ptr=ptr->link;
        pos++;
    }
    printf("Item %d not found in list\n",data);
}/*End of search() */
```

## 10.15.10 Reversing A Linked List

Let us take a linked list-

The link of second node should point to first node hence
`p2->link = p1;`
Now we will traverse the linked list with p3 pointer and shift pointers p1 and p2 forward. We set p1 to the link part of p2, so that link of each node will now point to its previous node.

```c
p2->link=p1;
while(p3!=NULL)
{
    p1=p2;
    p2=p3;
    p3=p3->link;
    p2->link=p1;
}
```

When this loop will terminate p3 will be NULL, p2 will point to last node, and link of each node now points to its previous node. Now start should point to the last node of the linked list, which is the first node of the reversed linked list.
`start = p2;`

![](img/a76c706396af8b310f291a5313a27079_334_0.png)

If the list contains only one element then there will be a problem in initializing p3, hence we check this condition in the beginning-

```c
if ( start->link == NULL )
return;
```

Here is the function reverse that reverses a linked list.

```c
reverse()
{
    struct node *p1,*p2,*p3;
    if(start->link==NULL) /*if only one element in the list*/
    return;
    p1=start;
    p2=p1->link;
    p3=p2->link;

    p1->link=NULL;
    p2->link=p1;

    while(p3!=NULL)
    {
        p1=p2;
        p2=p3;
        p3=p3->link;
        p2->link=p1;
    }
    start=p2;
}
/*End of reverse() */
```

## 10.16 union

Union is a derived data type like structure and it can also contain members of different data types. The syntax used for definition of a union, declaration of union variables and for accessing members is similar to that used in structures, but here keyword union is used instead of struct. The main difference between union and structure is in the way memory is allocated for the members. In a structure each member has its own memory location, whereas members of union share the same memory location. When a variable of type union is declared, compiler allocates sufficient memory to hold the largest member in the union. Since all members share the same memory location hence we can use only one member at a time. Thus union is used for saving memory. The concept of union is useful when it is not necessary to use all members of the union at a time.

The syntax of definition of a union is-

```c
union union_name{
    datatype member1;
    datatype member2;
    ...............
};
```

Like structure variables, the union variables can be declared along with the definition or separately. For example-

```c
union union_name{
    datatype member1;
    datatype member2;
    ...........
}variable_name;
```

This can also be declared as-
`union union_name variable_name;`

We can access the union members using the same syntax used for structures. If we have a union variable then the members can be accessed using dot(.) operator, and if we have a pointer to union then the members can be accessed using the arrow (->) operator.

```c
/*10.16 Program for accessing union members*/
#include<stdio.h>
main()
{
    union result{
        int marks;
        char grade;
        float per;
    }res;
    res.marks=90;
    printf("Marks : %d\n",res.marks);
    res.grade='A';
    printf("Grade : %c\n",res.grade);
    res.per=85.5;
    printf("Percentage : %f\n",res.per);
}
```

Output :

Marks : 90
Grade : A
Percentage : 85.500000

Before the first printf, the value 90 is assigned to the union member marks, so other members grade and per contain garbage value. After first printf, the value 'A' is assigned to the union member grade. So now the other two members marks and per contain garbage value. Only one member of union can hold value at a time, don't try to use all the members simultaneously. So a union variable of type result can be treated as either an int variable or char variable or a float variable. It is the responsibility of the programmer to keep track of member that currently holds the value.

Union variables can also be initialized, but there is a limitation. We know that due to sharing of memory all the members can't hold values simultaneously. So during initialization also only one member can be given an initial value, and this privilege is given to the first member. Hence only the first member of a union can be given an initial value. The type of the initializer should match with the type of the first member. For example, we can initialize the above union variable as-

```c
union result res ={78};
```

Now we'll take a program and compare the memory allocated for a union and structure variable

```c
/* P10.17 Program to compare the memory allocated for a union and structure variable*/
#include<stdio.h>
struct stag{
    char c;
    int i;
    float f;
};
union utag{
    char c;
    int i;
    float f;
};
main()
{
    union utag uvar;
    struct stag svar;
    printf("Size of svar = %u\n",sizeof(svar));
    printf("Address of svar : %u\t",&svar);
    printf("Address of members : %u %u %u\n",&svar.c,&svar.i,&svar.f);
    printf("Size of uvar = %u\n",sizeof(uvar));
    printf("Address of uvar : %u\t",&uvar);
    printf("Address of members : %u %u %u\n",&uvar.c,&uvar.i,&uvar.f);
}
```

Output :

Size of svar = 7
Address of svar : 65514 Address of members : 65514 65515 65517
Size of uvar = 4
Address of uvar : 65522 Address of members : 65522 65522 65522

![](img/a76c706396af8b310f291a5313a27079_337_0.png)

![](img/a76c706396af8b310f291a5313a27079_337_1.png)

The addresses of members of a union are same while the addresses of members of a structure are different. The difference in the sizes of variables svar and uvar also indicates that union is very economical in the use of memory. Note that the sizes of both union and structure variables may be affected by padding as discussed previously.

A structure may be a member of union or a union may be a member of structure. For example-

```c
union result
{
    int marks;
    char grade;
};
```

```c
struct res
{
    char name[15];
    int age;
    union result performance;
} data;
```

Here data is the structure variable of type struct res. It has three members, an array of characters name, an integer age and a union member performance. Union will take only one value at a time, either an integer value marks or a character value grade. This can also be written as-
