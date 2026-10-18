# DISPLAY 18.30 A Linked List of Nodes Using Smart Pointers (part 2 of 2)

```
39
40 shared_ptr<Node> Node::getNext()
41 {
42     return next;
43 }
44
45 void Node::setNext(shared_ptr<Node> nextPtr)
46 {
47     next = nextPtr;
48 }
49
50 void listTest()
51 {
52     shared_ptr<Node> root(new Node(10, nullptr));
53     shared_ptr<Node> next1(new Node(20, nullptr));
54     shared_ptr<Node> next2;
55     // After a shared_ptr is declared we can set it
56     // using the reset function
57     next2.reset(new Node(30, nullptr));
58     // Link the nodes together
59     root->setNext(next1);
60     next1->setNext(next2);
61
62     // Output the list
63     shared_ptr<Node> temp;
64     temp = root;
65     while (temp != nullptr)
66     {
67         cout << temp->getNum() << endl;
68         temp = temp->getNext();
69     }
70 }
71
72 int main()
73 {
74     listTest();
75     cout << "Exiting program." << endl;
76 }
```

# Sample Dialogue

```
10
20
30
Deleting 10
Deleting 20
Deleting 30
Exiting program.
```