```
void R_Traverse()
{
    Recursive_Traverse(Head);
    cout << endl;
}
void DeleteNode(int del_position);
};

void Llist :: ~Llist()
{
    Node *Temp;
    while(Head != Null)
    {
        Temp = Head;
        Head = Head->link;
        delete Temp;
    }
}

void Llist :: Create()
{
    char ans;
    Node *NewNode;
    while(1)
    {
        cout << "Any more nodes to be added (Y/N)*";
        cin >> ans;
        if(ans == 'n') break;
        NewNode = GetNode();
        Append(NewNode);
    }
}

void Llist :: Append(Node* NewNode)
{
    if(Head == Null)
    {
        Head = NewNode;
        Tail = NewNode;
    }
    else
    {
```