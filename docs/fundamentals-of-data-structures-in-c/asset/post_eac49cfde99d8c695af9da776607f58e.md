
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
    else if(p -> exp == head -> exp)
    {
        head -> coef = head -> coef + p -> coef;
        if(head -> coef == 0.0F)
            return head -> next;
    }
    return head;
}

void viewPoly(poly * ply)
{
    if(ply == NULL)
        printf("NULL\n");
    while(ply != NULL)
    {
        printf("%.2fx^%d", ply -> coef, ply -> exp);
        printf("%s", (ply -> next == NULL) ? " = 0\n" : " + ");
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

poly *mulNode(poly *p1, poly *p2)
{
    poly *temp = NULL;
    if(p1 != NULL)
    {
        temp = getNode();
        temp -> coef = p1 -> coef * p2 -> coef;
        temp -> exp = p1 -> exp + p2 -> exp;
        temp -> next = mulNode(p1->next, p2);
    }
    return temp;
}

/* For Quotient and Remainder p1 / p2 */

poly *polyDiv(poly *p1, poly *p2, poly **rmdr)
{
    poly *res = NULL;
    if(p1 == NULL || p2 == NULL)
        return (*rmdr = NULL);
    if(p1 -> exp >= p2 -> exp)
    {
        res = getNode();
        res -> coef = p1 -> coef / p2 -> coef;
        res -> exp = p1 -> exp - p2 -> exp;
        res -> next = polyDiv(polySub(p1,mulNode(p2,res)),p2,rmdr);
    }
    else
        *rmdr = p1;
    return res;
}
```

## The program displays the following output

- Polynomial Manipulation using singly linked list ...
- 0. View the Main Menu
- 1. Create the First Polynomial
- 2. Create the Second Polynomial
- 3. View the First and Second Polynomial
- 4. Polynomial Addition
- 5. Polynomial Subtraction
- 6. Polynomial Multiplication
- 7. Polynomial Division
- 8. Exit

? 3
The First Polynomial is ...
NULL
The Second Polynomial is ...
NULL
? 4
The Resultant Polynomial after Addition is ...
NULL
? 5
The Resultant Polynomial after Subtraction is ...
NULL
? 6
The Resultant Polynomial after Multiplication is ...
NULL
? 7
The Resultant Polynomial after Division is ...
Solution is Infinity ...
Solution is Infinity ...
Quotient : NULL
Remainder : NULL
? 1
Enter the First Polynomial . . .
Enter the Coefficient : 3
Enter the Exponent : 2
Enter the Coefficient : 2
Enter the Exponent : 1
Enter the Coefficient : 1
Enter the Exponent : 0
First Polynomial is : 3.00x^2 + 2.00x^1 + 1.00x^0 = 0
? 2
Enter the Second Polynomial . . .
Enter the Coefficient : 2
Enter the Exponent : 1
Enter the Coefficient : 3
Enter the Exponent : 1
Enter the Coefficient : 5
Enter the Exponent : 0
Second Polynomial is : 5.00x^1 + 5.00x^0 = 0

? 3
The First Polynomial is ...
3.00x^2 + 2.00x^1 + 1.00x^0 = 0
The Second Polynomial is ...
5.00x^1 + 5.00x^0 = 0
? 4
The Resultant Polynomial after Addition is ...
3.00x^2 + 7.00x^1 + 6.00x^0 = 0
? 5
The Resultant Polynomial after Subtraction is ...
3.00x^2 + -3.00x^1 + -4.00x^0 = 0
? 6
The Resultant Polynomial after Multiplication is ...
15.00x^3 + 25.00x^2 + 15.00x^1 + 5.00x^0 = 0
? 7
The Resultant Polynomial after Division is ...
Quotient : 0.60x^1 + -0.20x^0 = 0
Remainder : 2.00x^0 = 0
? 8
End of Run of your Program . . .

Program 3.8 is capable of reading input in any sequence, and at the same time, reading input with an exponent value of zero. If you enter the same value of exponent again and again, it will automatically add the coefficients of same exponent and store it in descending order. You can also change any one of the existing polynomial and manipulate (add, subtract, multiply, divide) the new polynomial with the old polynomial.

## Advantages of Linked Lists

- It is not necessary to specify the number of elements in a linked list during its declaration (since memory can be allocated dynamically when a node is added to the list).
- Linked list can grow and shrink in size depending upon the insertion and deletion that occurs in the list.
- Insertions and deletions at any place in a list can be handled easily and efficiently.
- A linked list does not waste any memory space.

## Disadvantages of Linked Lists

- Searching a particular element in a list is difficult and time consuming.
- A linked list will use more storage space than an array to store the same number of elements (. . . Each element in a list needs additional memory space for storing the address of the next node).

## 3.10 Summary

- Some of the important applications of linked lists are stacks and queues.
- Stacks can be implemented by arrays or linked lists.
- A stack is an ordered collection of elements in which insertions and deletions are restricted to one end. The end from which elements are added and/or removed is referred to as top of the stack.
- Stacks are referred to as Last-In-First-Out (LIFO) lists or piles or push-down lists.
- The primitive operations that can be carried out in a stack are push, pop and peek operations.
- Push is an operation used to add a new element into a stack.
- Pop is an operation used to remove the top most elements from the stack.
- Peek is an operation used to display the top most element from the stack.
- In array representation of stacks, if a stack contains no elements, it is referred to as an empty stack.
- In array representation of stacks, if a stack contains elements equal to its size, it is referred to as an fully occupied stack.
- In a linked list, if the stack is pointing to NULL the stack is said to be an empty stack.
- If the malloc function returns NULL in a linked list it is referred as an fully occupied stack.
- Some of the important applications of stacks are tower of hanoi, reversing a string, checking for balanced parenthesis and evaluation of arithmetic expressions.
- Towers of Hanoi is a game in which we are given a tower of n disks, initially stacked in increasing size from top to bottom. Next to this tower, we have two more towers. The objective is to transfer the entire disks from Tower 1 to entire Tower 3 using Tower 2.
- Given an arithmetic expression, what we exactly mean by balanced is that, an opening parenthesis of various shapes (parenthesis, a square brace, or a flower brace) must match the corresponding last unmatched closing parenthesis symbol of the same shape and all parenthesis symbols must be matched when the arithmetic expression is finished.
- The different notations for representing arithmetic expressions are infix, prefix and postfix notations.
- The normal way of expressing mathematical expressions is called as infix notation.
- Prefix notation also referred, as polish notation is a way of writing algebraic expressions without the use of parenthesis or rules of operator precedence.

Postfix notation also referred, as suffix form or reverse polish notation (or RPN) is also a way of writing algebraic expressions without the use of parentheses or rules of operator precedence.

A queue is an ordered collection of elements in which insertions are made at one end and deletion are made at the other end. The end at which insertions are made is referred to as the rear end, and the end from which deletions are made is referred to as the front end.

The primitive operations that can be carried out in a queue are enqueue and dequeue operations.

Enqueue is an operation used to add a new element into the rear end of a queue.

Dequeue is an operation used to remove an element from the front end of a queue.

Circular queue is another form of a linear queue in which the last node is connected to the first node of the list.

Deque (Double-ended queue) is another form of a queue in which insertions and deletions are made at both the front and rear ends of the queue.

There are two variations of a deque, namely input restricted deque and output restricted deque. The input restricted deque allows insertion at one end (it can be either front or rear) only. The output restricted deque allows deletion at one end (it can be either front or rear) only.

The implementation part of the circular queue is same as that of the linear queue, except that the last position is connected to the first position of the queue. So the front end and rear end moves circularly.

The implementation part of the circular deque is same as that of the linear deque, except that the last position is connected to the first position of the deque. So the front end and rear end moves circularly.

## 3.11 Short-answer Questions

- 1. Define a stack.

Stack is an ordered collection of elements in which insertions and deletions are restricted to one end. The end from which elements are added and/or removed is referred to as top of the stack. Stacks are also referred as “piles” and “push-down lists”.

- 2. List out the basic operations that can be performed on a stack and a queue.

The basic operations that can be performed on a stack and queue are,

- Push operation
- Pop operation
- View stack contents.
