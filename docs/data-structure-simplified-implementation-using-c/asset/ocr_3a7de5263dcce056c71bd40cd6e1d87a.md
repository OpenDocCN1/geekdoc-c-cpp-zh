```
first=new dnode;
first->data=element;
first->next=first;
first->prev=first;
end=first;
return;
} // end of if statement
dnode *newnode; //to create any other node
newnode=new dnode;
newnode->data=element;
newnode->next=end->next;
newnode->prev=end;
end->next=newnode;
first->prev=newnode;
end=newnode;
}
```

After inserting the node into the circular doubly link list, we need to view the data available in a circular doubly link list. This objective can be accomplished with the help of display function. In the display function, due diligence is to be exercised in order to avoid infinite looping. Since, in the circular doubly link list, last node is connected to the first node, therefore, loop must terminate at the ‘end’ node otherwise, it will lead to infinite loop.

```
void dblyList::display()
{
    dnode *current=first;
    while(current->next!=first)
    {
        cout<<current->data<<"->";
        current=current->next;
    }
    //to display the data of last node
    cout<<current->data<<"->";
}
```

# 4.9.3 To count the number of nodes in a circular doubly link list

To count the number of nodes in a circular doubly link list, we need to begin traversal either from the front or from the back. In a circular doubly link list since first is connected to the last