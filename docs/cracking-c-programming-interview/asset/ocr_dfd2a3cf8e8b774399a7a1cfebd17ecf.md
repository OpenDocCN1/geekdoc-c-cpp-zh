```
int SN;
char name[10];
struct addr loc;
};
int main()
{
    struct one objl = {1, "Ranbir" , 80 , 81 , 
    "Mandaky","Mumbai"}; // line 1
    printf("%s %d s", objl.name,objl.loc.h_no[0],
    objl.loc.city); // line 2
    return 0;
}
```

+   (a) error in structure one
(b) error in line1
(c) error at line 2
(d) Ranbir 80 Mumbai

# 53. What is the output of the following program?

```
#include<stdio.h>
struct node{
    int key1;
    int key2;
    struct node *next;
} s1;
struct nodetab{
    int hash;
    struct node* item;
    struct nodetab *next;
    int nt;
};
int main()
{
    printf("%ld %ld",sizeof(s1),sizeof(nt));
    return 0;
}
```