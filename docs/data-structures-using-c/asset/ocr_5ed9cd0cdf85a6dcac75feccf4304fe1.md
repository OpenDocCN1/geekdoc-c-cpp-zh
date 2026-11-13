```
{
 int val,pos;
 DList L2;
 L2.Create();
 L2.Traverse();
 cout << "Enter Node Data to be deleted-->";
 cin >> val;
 L2.DeleteNode( val );
 L2.Traverse();
 cout << "Enter Node position to be deleted-->";
 cin >> pos;
 L2.Delete_Pos(pos);
 L2.Traverse();
}
```

# 6.7.3 Insertion of a Node in a Doubly Linked List

Now, let us discuss inserting a node in DLL. To insert a node, say Current, we have to modify four links as each node points to its predecessor as well as successor. Let us assume that the node Current is to be inserted in between the two nodes say node1 and node2. We have to modify the following links:

node1-->Next, node2-->Prev, Current-->Prev, and Current-->Next

When the Current node is inserted in between node1 and node2, node1's successor node changes. Hence, we need to modify node1-->Next. For the node node2, its predecessor changes. Therefore, we need to modify node2-->Prev This is shown in Fig. 6.31.

![](bbox=[0.36, 0.65, 0.75, 0.83])

Fig. 6.31 Inserting a node current

Current is a new node to be inserted. We need to set both its predecessor and successor by setting the links as Current-->Prev and Current-->Next