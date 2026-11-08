```
```text
new1->insert_at_middle();
break;

case 4:
    clrscr();
    head->insert_at_end();
    break;

case 5:
    clrscr();
    head->delete_data();
    break;

case 8:
    head->display();
    break;

case 9:
    exit(0);
}
}while(1);
return 0;
```
```

In the next section, let’s learn about stacks.

# Stack

A stack can be defined as a linear data structure, where items are added one at a time and can only be removed in the reverse order in which they were entered. The last item added to the stack is called the *top* of the stack. Suppose we enter A, B, C and D in a stack, then D is the *top* and these items can be removed in the order D, C, B and A; therefore, a stack follows a LIFO strategy. The common operations done with a stack are adding an element into the stack and deleting an element from the stack. Adding an element in a stack is called *push*. Listing 24.5 shows the code to implement the *push* operation:

**Listing 24.5:** Implementing the Push Operation

```
```text
procedure add(item : items)
{add item to the global stack stack;
top is the current top of stack
and n is its maximum size}
begin
    if top = n then stackfull;
    top := top+1;
    stack(top) := item;
end; {of add}
```
```

Deleting an item from a stack is done by deleting the last element entered in the stack first. This operation is called *pop*. Listing 24.6 shows the implementation of the *pop* operation:

**Listing 24.6:** Implementing the Pop Operation

```
```text
procedure delete(var item : items)
{remove top element from the stack and put it in the item}
begin
    if top = 0 then stackempty;
    item := stack(top);
    top := top-1;
end; {of delete}
```
```