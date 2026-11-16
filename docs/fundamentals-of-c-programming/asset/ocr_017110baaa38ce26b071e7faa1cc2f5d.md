The value `nullptr` in a Boolean context is considered `false`, so we can simplify the Boolean expression `cursor != nullptr` to just `cursor`; this allows us to simplify the loop somewhat, as

```
// Print the linked list built from the Node objects
for (Node *cursor = &n1; cursor = cursor->next)
    std::cout << cursor->data << ' ';
```

Since we hard-coded the four list nodes into the program's source, the loop really is not necessary. The following statement:

```
std::cout << n1.data << ' ' << n2.data << ' ' << n3.data
     << n4.data << '\n';
```

is simpler, but why stop there? Since we know the nodes and their values ahead of time, the following statement is even simpler:

```
std::cout << "23 10 0 3\n";
```

The hard-coded list in Figure 18.2 and Listing 18.2 (manualinkedlist.cpp) does not demonstrate the utility possible to the dynamic nature of linked lists. It makes sense to use a linked list only when its elements are unknown ahead of time. We then can dynamically allocate space for the elements as they become available.

Armed with our knowledge of C++ classes, encapsulation, and methods, we can build a client-friendly, dynamic linked list type. The code found in Listing 18.3 (intlist1.h), Listing 18.4 (intlist1.cpp), and Listing 18.5 (listmain.cpp) demonstrates the power of linked lists. Listing 18.3 (intlist1.h) is the header file for a simple integer linked list class.

# Listing 18.3: intlist1.h

```
class IntList1 {
    /*
     * An object that holds an element in a linked list.
     * This type is local to the IntList1 class and inaccessible
     * to outside this class.
     */
    struct Node {
        int data;      // A data element of the list
        Node *next;    // The node that follows this one in the list
        Node(int d);   // Constructor
    };

    Node *head;   // Points to the first item in the list
    Node *tail;   // Points to the last item in the list

    /*
     * Returns the length of the linked list pointed to by p.
     */
    int length(Node *p) const;

    /*
     * dispose(p)
     * Deallocate the memory held by the list pointed to by p.
     */
    void dispose(Node *p);
```