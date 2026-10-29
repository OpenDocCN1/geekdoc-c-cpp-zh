```
```cpp
Node::Node(int numVal, shared_ptr<Node> nextPtr) : num(numVal),
next(nextPtr)
{
}

int Node::getNum()
{
        return num;
}

shared_ptr<Node> Node::getNext()
{
        return next;
}

void Node::setNext(shared_ptr<Node> nextPtr)
{
        next = nextPtr;
}

void listTest()
{
        shared_ptr<Node> root(new Node(10, nullptr));
        shared_ptr<Node> next1(new Node(20, nullptr));
        shared_ptr<Node> next2;
        // After a shared_ptr is declared we can set it
        // using the reset function
        next2.reset(new Node(30, nullptr));
        // Link the nodes together
        root->setNext(next1);
        next1->setNext(next2);

        // Output the list
        shared_ptr<Node> temp;
        temp = root;
        while (temp != nullptr)
        {
                cout << temp->getNum() << endl;
                temp = temp->getNext();
        }
}

int main()
{
        listTest();
        cout << "Exiting program." << endl;
        return 0;
}
```
```