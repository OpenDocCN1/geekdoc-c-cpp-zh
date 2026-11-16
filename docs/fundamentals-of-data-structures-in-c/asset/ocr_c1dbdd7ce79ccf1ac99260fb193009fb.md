```
while(poly2 != NULL)
{
    head = insertNode(head, copyNode(poly2, POSITIVE));
    poly2 = poly2 -> next;
}
    return head;
}
poly * polySub(poly *poly1, poly *poly2)
{
    poly *head = NULL;
    while(poly1 != NULL)
    {
        head = insertNode(head, copyNode(poly1, POSITIVE));
        poly1 = poly1 -> next;
    }
    while(poly2 != NULL)
    {
        head = insertNode(head, copyNode(poly2, NEGATIVE));
        poly2 = poly2 -> next;
    }
    return head;
}
poly * polyMul(poly *poly1, poly *poly2)
{
    if(poly2 == NULL)
        return NULL;
    else
        return polyAdd(mulNode(poly1,poly2),polyMul(poly1,poly2->next));
}
poly * copyNode(poly * p, int sign)
{
    poly *newnode;
    newnode = getNode();
    newnode -> coef = sign * p -> coef;
    newnode -> exp = p -> exp;
    newnode -> next = NULL;
    return newnode;
}
```