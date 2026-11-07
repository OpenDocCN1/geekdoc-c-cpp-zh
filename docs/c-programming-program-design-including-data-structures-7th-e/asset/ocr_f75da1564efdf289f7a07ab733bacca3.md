```
```cpp
template <class Type>
class doublyLinkedList
{
public:
    const doublyLinkedList<Type>& operator=
                              (const doublyLinkedList<Type>&);
    //Overload the assignment operator.

    void initializeList();
       //Function to initialize the list to an empty state.
       //Postcondition: first = nullptr; last = nullptr; count = 0;

    bool isEmptyList() const;
       //Function to determine whether the list is empty.
       //Postcondition: Returns true if the list is empty,
       //               otherwise returns false.

    void destroy();
       //Function to delete all the nodes from the list.
       //Postcondition: first = nullptr; last = nullptr; count = 0;

    void print() const;
       //Function to output the info contained in each node.

    void reversePrint() const;
       //Function to output the info contained in each node
       //in reverse order.

    int length() const;
       //Function to return the number of nodes in the list.
       //Postcondition: The value of count is returned.

    Type front() const;
       //Function to return the first element of the list.
       //Precondition: The list must exist and must not be empty.
       //Postcondition: If the list is empty, the program
       //               terminates; otherwise, the first
       //               element of the list is returned.

    Type back() const;
       //Function to return the last element of the list.
       //Precondition: The list must exist and must not be empty.
       //Postcondition: If the list is empty, the program
       //               terminates; otherwise, the last
       //               element of the list is returned.

    bool search(const Type& searchItem) const;
       //Function to determine whether searchItem is in the list.
       //Postcondition: Returns true if searchItem is found in
       //               the list, otherwise returns false.
};
```
```