```
char name[30]
    struct *next;
};
typedef struct node;
```

6.30 The following code is defined in a header file list.h
typedef struct {
  char name[15];
  int age;
  float weight;
}DATA;
struct linked_list {
  DATA person;
  struct linked_list *next;
};
typedef struct linked_list NODE;
typedef NODE *NDPTR;
Explain how could we use this header file for writing programs.

6.31 What does the following code achieve?
int * p;
p = malloc (sizeof (int) );

6.32 What does the following code do?
float *p;
p = calloc (10,sizeof(float) );

6.33 What is the output of the following code?
int i, *ip;
ip = calloc ( 4, sizeof(int) );

```
for (i = 0 ; i < 4 ; i++)
  * ip++ = i * i;
for (i = 0 ; i < 4 ; i < 4)
  printf("%d\n", *--ip );
```

6.34 What is printed by the following code?
int *p;
p = malloc (sizeof (int) );
*p = 100 ;
p = malloc (sizeof (int) );
*p = 111;
printf("%d", *p);

6.35 What is the output of the following segment?
struct node {
  int m ;
  struct node *next;
} x, y, z, *p;
x.m = 10 ;
y.m = 20 ;
z.m = 30 ;
x.next = &y;
y.next = &z;
z.next = NULL;
p = x.next;
while (p != NULL)
{
  printf("%d\n", p -> m);
  p = p -> next;
}

# Programming Exercises

+   6.1 Write a program using pointers to read in an array of integers and print its elements in reverse order.
+   6.2 We know that the roots of a quadratic equation of the form ax² + bx + c = 0 are given by the following equations:
+     x1 = (-b + square-root(b² - 4ac)) / 2a
+     x2 = (-b - square-root(b² - 4ac)) / 2a
+   Write a function to calculate the roots. The function must use two pointer parameters, one to receive the coefficients a, b, and c, and the other to send the roots to the calling function.
+   6.3 Write a function that receives a sorted array of integers and an integer value, and inserts the value in its correct place.
+   6.4 Write a function using pointers to add two matrices and to return the resultant matrix to the calling function.
+   6.5 Using pointers, write a function that receives a character string and a character as argument and deletes all occurrences of this character in the string. The function should return the corrected string with no holes.
+   6.6 Write a function day_name that receives a number n and returns a pointer to a