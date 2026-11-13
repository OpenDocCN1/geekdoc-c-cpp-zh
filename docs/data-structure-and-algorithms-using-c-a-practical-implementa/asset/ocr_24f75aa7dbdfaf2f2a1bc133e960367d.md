+   STEP-3: IF (P2 = NULL)
+   REPEAT WHILE (P1 != NULL)
+   ADD(P3,DEGREE(P1),COEF(P1))
+   P1 := NEXT(P1)
+   [END OF LOOP]
+   [END OF IF]
+   STEP - 4: RETURN

# ADD(P3,COEF,EXP)

+   STEP-1: ALLOCATE A MEMORY TO P3->NEXT
+   STEP-2: P3 := NEXT[P3]
+   STEP-3: COEF[P3] := COEF
+   EXP[P3] := EXP
+   STEP-4: NEXT[P3] := NULL
+   STEP-5: RETURN

# 7.9.2 /* Polynomial With Help of Linked List */

```
# include <stdio.h>
# include <alloc.h>
struct link
{
int coef;
int expo;
struct link *next;
};
int i;
int number;
struct link *start, *previous, *new;
void create(struct link *node)
{
char ch='y';
start.next = NULL; /* Empty list /*
node = &start; /* Point to the start of the list /*
i = 0;
while(ch == 'y' || ch=='Y')
{
node->next = (struct link * )
malloc(sizeof(struct link));
node = node->next;
printf("\nENTER THE COEFFICIENT VALUE:");
fflush(stdin);
scanf("%d", &node->coef);
printf("\nENTER THE EXPONENT VALUE:");
```