```
printf( "%d", node->info );
    node = node->next;
}
}
void create( struct link *node)
{
    int i;
    int no;
    printf( "\n Input the number of nodes you want to create." );
    scanf( "%d", &no );
    for ( i = 0; i < no ; i++)
    {
        printf( "\nEnter the number" );
        scanf( "%d", &node->info );
        node->next = ( struct link * ) malloc( sizeof( struct link ) );
        if ( i == no - 1)
            node->next = NULL;
        else
            node = node->next;
    }
    node->next = NULL;
}
```

# 7.4.13 Program for Student Data Using Linked List

```
# include<iostream>
# include<fstream>
# include<stdlib.h>
# include<conio.h>
using namespace std;
struct student
{
    string fname,lname;
    int yob,mob,dob;
    char sex;
    float mark;
    struct student *next;
};
struct student start,*last,*New;
//method declarations
void insert(struct student *);
void create(struct student *);
void display(struct student *);
void average(struct student *);
void maximum(struct student *);
void search(struct student *);
```