
sl.grade = 'A';
printf("%c %ld",sl.grade,sizeof(sl));//line 3
char *p = &sl; //line 4
*p = 10; //line 5
p += 4;
*p = 'B'; //line 7
printf("%d %c",sl.SN,sl.grade); // line 8
return 0;
}
```

- (a) error- compile time
- (b) A 5 10 B
- (c) A 8 10 A
- (d) A 8 10 B

# 50. What is the output of the following program?

```c
struct student {
int roll;
struct dob{
int dd;
int mm;
int yyyy;
};
sl;
int main() 
{
sl.roll = 1;
sl.dob.dd = 6;
sl.dob.mm = 1;
sl.dob.yyyy = 2006;
printf("%d %ld",sl.dob.yyyy,sizeof(sl));
return 0;
}
```

- (a) 2006 16
- (b) 2006 12
- (c) error in structure declaration
- (d) error in main function

# 51. What is the output of the following program?

```c
struct student {
  int roll;
  struct dob{
    int dd;
    int mm;
    int yyyy;
  } u;
} sl;
int main() {
  sl1.roll = 1;
  sl1.dd = 6;
  sl1.u.mm = 1;
  sl1.u.yyyy = 2006;
  printf("%d %ld",sl1.u.yyyy,sizeof(sl1));
  return 0;
}
```

- (a) 2006 16
- (b) 2006 24
- (c) error- compile time in structure declaration
- (d) error- compile time in main function

# 52. What is the output of the following program?

```c
#include<stdio.h>
#include<stdlib.h>
struct addr{
  int h_no[2];
  char streat[40];
  char city[40];
};
struct one {
int SN;
char name[10];
struct addr loc;
};
int main()
{
    struct one objl = {1, "Ranbir" , 80 , 81, 
    "Mandaky","Mumbai"}; // line 1
    printf("%s %d s", objl.name,objl.loc.h_no[0],
    objl.loc.city); // line 2
    return 0;
}
```

- (a) error in structure one
- (b) error in line1
- (c) error at line 2
- (d) Ranbir 80 Mumbai

# 53. What is the output of the following program?

```c
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

- (a) 12 20
- (b) 16 40
- (c) error- compile time
- (d) 12 12

54. Consider the above program's structure here also. What is the output of the following program?

```c
#include<stdio.h>
struct node fun(struct node);
int main()
{
    struct node s1 , s2;
    s1.key1 = 10;
    s1.key2 = 20;
    s1.next = NULL;
    s2 = fun(s1);
    printf("%d %d",s1.key1,s1.key2);
    printf("%d %d",s2.key1,s2.key2);
    return 0;
}
struct node fun(struct node s3)
{
    s3.key1 = s3.key1^s3.key2;
    s3.key2 = s3.key1^s3.key2;
    s3.key1 = s3.key1^s3.key2;
    return s3;
}
```

- (a) 20 10 20 10
- (b) error- compile time
- (c) the fun function produces compiler dependent output
- (d) the fun function always swaps key1 and key2 of s3.

55. What is the output of the following program?
```c
#include<stdio.h>
#include<string.h>

struct student{
int roll;
char name[10];
int getRoll(struct student *sl){
  return sl->roll;
}
void show(struct student *sl){
  printf("%d %s",sl->roll,sl->name);
}
struct student sl;
int main()
{
  sl.roll = 10;
  strcpy(sl.name, "john");
  show(&sl);
  int i = getRoll(&sl);
  printf("%d %ld",i,sizeof(sl));
  return 0;
}
```

- (a) 10 john 10 16
- (b) 10 john 10 14
- (c) 10 john 10 24
- (d) error- compile time

56. What is the output of the following code?

```c
#include<stdio.h>
union{
int a;
int b;
struct {
  char name[4];
} sl;
} ul;
int main()
{
ul.a = 67;
ul.b = 68;
printf("%ld %s", sizeof(ul), ul.sl.name);
return 0;
}
```

- (a) 8
- (b) 4
- (c) error- compile time
- (d) 12

57. What is the output of the following program?

```c
#include<stdio.h>
struct student {
char *name;
} sl;
int main()
{
strcpy(sl.name, "john"); // line 1
printf("%s",sl.name); // line 2
sl.name[0] = 'T'; // line 3
return 0;
}
```

- (a) john
- (b) error at line 1
- (c) error at line 2
- (d) error at line 3

58. What is the output of the following program?

```c
#include<stdio.h>
#include<stdlib.h>
struct node{
int key1;
int key2;
};
void swap(struct node *start)
{
    struct node *root = malloc(sizeof(struct node));
    root->key1 = 10;
    root->key2 = 20;
    root->key1 = root->key1^root->key2;
    root->key2 = root->key1^root->key2;
    root->key1 = root->key1^root->key2;
    start = root; // line 8
}
int main()
{
    struct node *start = malloc(sizeof(struct node)*2);
    start = NULL; // line 12
    swap(start);
    printf("%d %d",start->key1,start->key2);
    return 0;
}
```

- (a) 20 10
- (b) 10 20
- (c) garbageValue
- (d) error- run time

59. What modifications require in the above code such that the swap function correctly swaps the numbers?

60. Determine the output of the following program?

```c
#include<stdio.h>
struct student{
    int roll;
    int class_no;
};
void foo(struct student temp)
{
    static struct student sl = {44, 1};
    sl.roll++;
    sl.class_no++;
    temp = sl;
    printf("%d %d", sl.roll, sl.class_no);
}
int main()
{
    struct student sl = {50, 50};
    int i;
    for(i = 1; i < 5; i++)
    foo(sl);
    printf("%d %d", sl.roll, sl.class_no);
    return 0;
}
```

# Other important questions for the Interview are as follows:

1. Write a C program to copy a tree.
2. Write a C program to create a mirror of a tree.
3. Write a C program for the in-order traversal of a tree without using recursion.
4. Write a C program for pre-order traversal of a tree without using recursion.
5. Write a C program for post-order traversal of a tree without using recursion.
6. Write a C program for finding the diameter of a tree.
7. Write a C program for finding the height of a tree.
8. Write a C program that gives the least common ancestor of two nodes in a tree.
9. Write a C program for the level order traversal of a tree.
10. Write a C program that finds root to leaf path for each leaf node.
11. Write a C program that finds the sum of all roots to the leaf node.
12. Write a C program for constructing a tree for which in-order and pre-order are given.
13. Write a C program for constructing a tree for which in-order and post-order are given.
14. Write a C program that accepts information of 'n' employees and displays it using structure (name, department, age, salary).
15. Write a C program for constructing a full binary tree.

# Group-7 Explanations

1. d

Explanation:

![](img/192d581e3a01f0e6c194cfc2ff02d9)
