```
```c
poly *insertNode(poly *head, poly *p)
{
    if(p -> coef == 0.0F)
        return head;
    if(head == NULL)
        return p;
    else if(p -> exp > head -> exp)
    {
        p -> next = head;
        return p;
    }
    else if(p -> exp < head -> exp)
        head -> next = insertNode(head -> next, p);
    else if(head -> coef = head -> coef + p -> coef == 0.0F)
        return head -> next;
    return head;
}

void viewPoly(poly * ply)
{
    if(ply == NULL)
        printf("NULL \\n");
    while(ply != NULL)
    {
        printf("%%.2fX^%d", ply -> coef, ply -> exp);
        printf("%s", (ply -> next == NULL) ? " = 0\\n" : " + ");
        ply = ply -> next;
    }
}

poly * polyAdd(poly *poly1, poly *poly2)
{
    poly *head = NULL;
    while(poly1 != NULL)
    {
        head = insertNode(head, copyNode(poly1, POSITIVE));
        poly1 = poly1 -> next;
    }
```
```