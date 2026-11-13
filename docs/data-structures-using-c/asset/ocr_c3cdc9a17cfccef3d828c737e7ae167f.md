```
PolyNode *link;
};

class Poly
{
private:
    PolyNode *Head, *Tail;
public:
    Poly() { Head = Tail = Null; } // constructor
    void Create();
    PolyNode *GetNode();
    void Append(PolyNode* NewNode);
    void Display();
    Poly PolyMult(Poly A);
    Poly PolyAdd(Poly A);
    void Insert(PolyNode*);
    int Evaluate(int val );
};

void Poly :: Create()
{
    char ans;
    PolyNode *NewNode;
    while(1)
    {
        cout << "Any term to be added? (Y/N)\n";
        cin >> ans;
        if(ans == 'N' || ans == 'n')
            break;
        NewNode = GetNode();
        if(Head == Null)
        {
            Head = NewNode;
            Tail = NewNode;
        }
        else
            Append(NewNode);
    }
}

void Poly :: Append(PolyNode* NewNode)
{
    if(Tail == Null)
        Head = Tail = NewNode;
```