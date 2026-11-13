```
};

class DList
{
private:
    DLL_Node *Head, *Tail;
public:
    DList()
    {
        Head = Tail = Null;
    }

    void Create();
    DLL_Node* GetNode();
    void Append(DLL_Node* NewNode);
    void Traverse();
    void DeleteNode(int val);
    void Delete_Pos(int pos);
    void Insert_Before(int val);
    void Insert_After(int val);
    void Insert_Pos(DLL_Node *NewNode, int pos);
};

DLL_Node* DList :: GetNode()
{
    DLL_Node *Newnode,
    Newnode = new DLL_Node;
    cout << "Enter Data";
    cin >> Newnode->Data;
    Newnode->Next = Newnode->Prev = Null;
    return(Newnode);
}

void DList :: Append(DLL_Node* NewNode)
{
    if(Head == Null)
    {
        Head = NewNode;
        Tail = NewNode;
    }
```