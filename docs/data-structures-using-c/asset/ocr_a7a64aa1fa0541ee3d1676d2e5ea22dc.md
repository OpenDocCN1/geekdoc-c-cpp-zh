```
PROGRAM CODE 7.14
// function to create inorder threaded binary search tree
void ThreadedBinaryTree :: create()
{
    Char ans;
    int flag;
    TEPTNode *node, *temp;
    Head = new TEPTNode;     // create head
    Head->Left = Head;
    Head->Right = Head;
    Head->Rbit = Head->Lbit = 1;
    // create root node for TBST
    Root = new TEPTNode;
    cout << "\n Enter data for root";
    cin >> Root->data;
    Root->Left = Head;
    Root->Right = Head;
    // attach root to left of Head
    Head->Left = Root;
    // make left thread bit of root 0
    Root->Lbit = Root->Rbit = 0;
    do
    {
        // create new node for a tree
        node = newTEPTNode;
        cout << "\n Enter data";
        cin >> node->data;
        node->Lbit = node->Rbit = 1;
        temp = Root;
        while
        {
            if(node->data < temp->data)
            {
                if(temp->Lbit == 1)
                {
                    // check leaf node and attach
                    {
                    node->Left = temp->Left;
                    node->Right = temp;
                    // attach to left of temp
                    temp->Lbit = 0;
```