
## Algorithm for Polynomial Addition

```pseudocode
POLYADD(POLY1 : POLY, POLY2 : POLY)
HEAD : POLY
Step 1 : Assign HEAD = NULL
Step 2 : While (POLY1 != NULL)
Step 3 : HEAD = INSERTNODE(HEAD, COPYNODE(POLY1, 1) )
Step 4 : POLY1 -> NEXT
Step 5 : [End of Step 2 While Structure]
Step 6 : While (POLY2 != NULL)
Step 7 : HEAD = INSERTNODE(HEAD, COPYNODE(POLY2, 1) )
Step 8 : POLY2 -> NEXT
Step 9 : [End of Step 6 While Structure]
Step 10 : Return HEAD
END POLYADD()
```

The following procedure is used to subtract two polynomials using singly linked lists.

- Using function polySub() subtract the two polynomials with the following comparisons.
- Copy the first polynomial using the functions copyNode() and insertNode() into the resultant polynomial.
- Traverse each term of second polynomial and insert them into the resultant polynomial using the functions copyNode() and insertNode() until NULL value of the second polynomial is reached. (Note: The second polynomial is inserted into the resultant polynomial by changing the sign of the coefficients using the function copyNode().)
- Display the resultant polynomial.

## Algorithm for Polynomial Subtraction

```pseudocode
POLYSUB(POLY1 : POLY, POLY2 : POLY)
HEAD : POLY
Step 1 : Assign HEAD = NULL
Step 2 : While (POLY1 != NULL)
Step 3 : HEAD = INSERTNODE(HEAD, COPYNODE(POLY1, 1) )
Step 4 : POLY1 -> NEXT
Step 5 : [End of Step 2 While Structure]
Step 6 : While (POLY2 != NULL)
Step 7 : HEAD = INSERTNODE(HEAD, COPYNODE(POLY2, -1) )
Step 8 : POLY2 -> NEXT
Step 9 : [End of Step 6 While Structure]
Step 10 : Return HEAD
END POLYSUB()
```

The following procedure is used to multiply two polynomials using singly linked lists.

- Using the function PolyMul() multiply two polynomials with the following comparisons.
- Traverse each term of the second polynomial and multiply with each term of the first polynomial using the function mulNode() and insert them into the resultant polynomial using the functions copyNode() and insertNode() until NULL value of the second polynomial is reached.
- Display the resultant polynomial.

## Algorithm for Multiplying the Multiplicant Polynomial by the Multiplier Node

```pseudocode
MULNODE(P1 : POLY, P2 : POLY)
TEMP : POLY
Step 1 : Assign TEMP = NULL
Step 2 : If (P1 != NULL) Then
    TEMP = GETNODE()
    TEMP -> COEF = P1 -> COEF * P2 -> COEF
    TEMP -> EXP = P1 -> EXP + P2 -> EXP
    TEMP -> NEXT = MULNODE(P1 -> NEXT, P2)
    [End of if Structure]
Step 3 : Return TEMP
END MULNODE()
```

## Algorithm for Polynomial Multiplication

```pseudocode
POLYMUL(P1 : POLY, P2 : POLY)
Step 1 : If (P2 == NULL) Then
    Return NULL
    [End of If Structure]
Step 2 : Return POLYADD(MULNODE(P1,P2), POLYMUL(P1, P2->NEXT))
END POLYMUL()
```

The following procedure is used to divide two polynomials using singly linked lists.

- The function polyDiv() is used to find the quotient and remainder of the divisor (The function returns the quotient value and assigns the remainder value to the argument in the function).
- If the dividend or divisor is NULL, assign the value of the remainder as NULL and return the value of the quotient as NULL.
- If the first exponent of the dividend is greater than or equal to the first exponent of the divisor,
  - The first coefficient of the dividend is divided by the first coefficient of the divisor, and the first exponent of the dividend is subtracted from the first exponent of the divisor and the corresponding coefficient and exponent is assigned to the resultant polynomial.
- Using the function mulNode() multiply the resultant polynomial with the divisor and subtract the result with the dividend using the function polySub() to get the remainder.
- The function polyDiv() is called recursively with the remainder as the new dividend until the above condition for the division fails.
- If the above condition for the division fails, return the resultant polynomial and assign the dividend value as the remainder.

## Algorithm for Polynomial Division

```pseudocode
POLYDIV(P1 : POLY, P2 : POLY, RMDR : POLY)
RES : POLY
Step 1 : Assign RES = NULL
Step 2 : If (P1 == NULL || P2 == NULL) Then
         Set RMDR = NULL
         Return NULL
         [End of If Structure]
Step 3 : If (P1 -> EXP >= P2 -> EXP) Then
         RES = GETNODE()
         RES -> COEF = P1 -> COEF / P2 -> COEF
         RES -> EXP = P1 -> EXP - P2 -> EXP
         RES -> NEXT = POLYDIV(POLYSUB(P1, MULNODE(P2, RES)), P2, RMDR)
         Else
         RMDR = P1
         [End of If Structure]
Step 4 : Return RES
END POLYDIV()
```

## Program 3.7

```c
/* Program to demonstrate polynomial manipulation using singly linked lists. */
/* polymani.c */
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
#define POSITIVE 1
#define NEGATIVE -1
typedef struct node
{
    float coef;
    int exp;
    struct node *next;
}poly;

void viewMenu();
void readNode(poly *);
void viewPoly(poly *);
poly *getNode();
poly *createPoly();
poly *copyNode(poly *, int);
poly *insertNode(poly *, poly *);
poly *mulNode(poly *p1, poly *p2);
poly *polyAdd(poly *p1, poly *p2);
poly *polySub(poly *p1, poly *p2);
poly *polyMul(poly *p1, poly *p2);
poly *polyDiv(poly *p1, poly *p2, poly **rmdr);
void main()
{
    int choice;
    poly *poly1 = NULL, *poly2 = NULL, *res = NULL;
    poly *Quotient, *Remainder = NULL;
    viewMenu();
    while(1)
    {
        printf("\n ? ");
        fflush(stdin);
        scanf("%d", &choice);
        switch(choice)
        {
            case 0 :
                viewMenu();
                break;
            case 1 :
                printf("\n Enter the First Polynomial ...");
                poly1 = createPoly();
                printf("\n First Polynomial is : ");
                viewPoly(poly1);
                break;
            case 2 :
                printf("\n Enter the Second Polynomial ...");
                poly2 = createPoly();
                printf("\n Second Polynomial is : ");
                viewPoly(poly2);
                break;
            case 3 :
                printf("\n The First Polynomial is ... \n");
                viewPoly(poly1);
                printf("\n The Second Polynomial is ... \n");
                viewPoly(poly2);
                break;
            case 4 :
                printf("\n The Resultant Polynomial after Addition is ... \n");
                res = polyAdd(poly1, poly2);
                viewPoly(res);
                break;
            case 5 :
                printf("\n The Resultant Polynomial after Subtraction is ... \n");
                res = polySub(poly1, poly2);
                viewPoly(res);
                break;
            case 6 :
                printf("\n The Resultant Polynomial after Multiplication is ... \n");
                res = polyMul(poly1, poly2);
                viewPoly(res);
                break;
            case 7 :
                printf("\n The Resultant Polynomial after Division is ... \n");
                Quotient = polyDiv(poly1, poly2, &Remainder);
                printf("\n Quotient : ");
                viewPoly(Quotient);
                printf("\n Remainder : ");
                viewPoly(Remainder);
                break;
            default :
                printf("\n End of Run of your Program . . ");
                exit(0);
        }
    }
}

void viewMenu()
{
    printf("\n\n Polynomial Manipulation using singly linked list ...");
    printf("\n\n\t 0. View the Main Menu");
    printf("\n\n\t 1. Create the First Polynomial");
    printf("\n\n\t 2. Create the Second Polynomial");
    printf("\n\n\t 3. View the First and Second Polynomial");
    printf("\n\n\t 4. Polynomial Addition");
    printf("\n\n\t 5. Polynomial Subtraction");
    printf("\n\n\t 6. Polynomial Multiplication");
    printf("\n\n\t 7. Polynomial Division");
    printf("\n\n\t 8. Exit");
}
poly *createPoly()
{
    poly *p, *head = NULL;
    do
    {
        p = getNode();
        readNode(p);
        head = insertNode(head, p);
    }while(p->exp != 0);
    return head;
}
poly *getNode()
{
    return (poly *)malloc(sizeof(poly));
}
void readNode(poly* newnode)
{
    int exp;
    float coef;
    printf("\nEnter the Coefficient : ");
    scanf("%f", &coef);
    printf("Enter the Exponent : ");
    scanf("%d", &exp);
    newnode->coef = coef;
    newnode->exp = exp;
    newnode->next = NULL;
}
