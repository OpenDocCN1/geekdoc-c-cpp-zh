
- 3. Extend the `class linkedListType` by adding the following operations:
  - a. Write a function that returns the info of the kth element of the linked list. If no such element exists, terminate the program.
  - b. Write a function that deletes the kth element of the linked list. If no such element exists, terminate the program.

  Provide the definitions of these functions in the `class linkedListType`. Also, write a program to test these functions. (Use either the `class unorderedLinkedList` or the `class orderedLinkedList` to test your function.)

- 4. **(Printing a single linked list backward)** Include the functions `reversePrint` and `recursiveReversePrint`, as discussed in this chapter, in the `class linkedListType`. Also, write a program function to print a (single) linked list backward. (Use either the `class unorderedLinkedList` or the `class orderedLinkedList` to test your function.)

- 5. **(Dividing a linked list into two sublists of almost equal sizes)**
  - a. Add the operation `divideMid` to the `class linkedListType` as follows:

    ```cpp
    void divideMid(linkedListType<Type> &subList);
    //This operation divides the given list into two sublists
    //of (almost) equal sizes.
    //Postcondition: first points to the first node and last
    //               points to the last node of the first
    //               sublist.
    //               subList.first points to the first node
    //               and subList.last points to the last node
    //               of the second sublist.
    ```

    Consider the following statements:

    ```cpp
    unorderedLinkedList<int> myList;
    unorderedLinkedList<int> subList;
    ```

    Suppose `myList` points to the list with elements 34 65 27 89 12 (in this order). The statement:

    ```cpp
    myList.divideMid(subList);
    ```

    divides `myList` into two sublists: `myList` points to the list with the elements 34 65 27, and `subList` points to the sublist with the elements 89 12.

  - b. Write the definition of the function template to implement the operation `divideMid`. Also, write a program to test your function.

- 6. **(Splitting a linked list, at a given node, into two sublists)**
  - a. Add the following operation to the `class linkedListType`:

    ```cpp
    void divideAt(linkedListType<Type> &secondList,
                  const Type& item);
    //Divide the list at the node with the info item into two
    //sublists.
    //Postcondition: first and last point to the first and
    //               last nodes of the first sublist.
    //               secondList.first and secondList.last
    //               point to the first and last nodes of the
    //               second sublist.
    ```

    Consider the following statements:

    ```cpp
    unorderedLinkedList<int> myList;
    unorderedLinkedList<int> otherList;
    ```

    Suppose myList points to the list with the elements 34 65 18 39 27 89 12 (in this order). The statement:

    ```cpp
    myList.divideAt(otherList, 18);
    ```

    divides myList into two sublists: myList points to the list with the elements 34 65, and otherList points to the sublist with the elements 18 39 27 89 12.

  - b. Write the definition of the function template to implement the operation `divideAt`. Also, write a program to test your function.

- 7. a. Add the following operation to the `class orderedLinkedList`:

    ```cpp
    void mergeLists(orderedLinkedList<Type> &list1,
                    orderedLinkedList<Type> &list2);
    //This function creates a new list by merging the
    //elements of list1 and list2.
    //Postcondition: first points to the merged list
    //               list1 and list2 are empty
    ```

    Consider the following statements:

    ```cpp
    orderedLinkedList<int> newList;
    orderedLinkedList<int> list1;
    orderedLinkedList<int> list2;
    ```

    Suppose list1 points to the list with the elements 2 6 7, and list2 points to the list with the elements 3 5 8. The statement:

    ```cpp
    newList.mergeLists(list1, list2);
    ```

    creates a new linked list with the elements in the order 2 3 5 6 7 8, and the object `newList` points to this list. Also, after the preceding statement executes, `list1` and `list2` are empty.

  - b. Write the definition of the function template `mergeLists` to implement the operation `mergeLists`.

- 8. The function `insert` of the class `orderedLinkedList` does not check if the item to be inserted is already in the list; that is, it does not check for duplicates. Rewrite the definition of the function `insert` so that before inserting the item, it checks whether the item to be inserted is already in the list. If the item to be inserted is already in the list, the function outputs an appropriate error message. Also, write a program to test your function.

- 9. In this chapter, the class to implement the nodes of a linked list is defined as a `struct`. The following rewrites the definition of the `struct` `nodeType` so that it is declared as a class and the member variables are private.

  ```cpp
  template <class Type>
  class nodeType
  {
  public:
      const nodeType<Type>& operator=(const nodeType<Type>&);
          //Overload the assignment operator.

      void setInfo(const Type& elem);
          //Function to set the info of the node.
          //Postcondition: info = elem;

      Type getInfo() const;
          //Function to return the info of the node.
          //Postcondition: The value of info is returned.

      void setLink(nodeType<Type> *ptr);
          //Function to set the link of the node.
          //Postcondition: link = ptr;

      nodeType<Type>* getLink() const;
          //Function to return the link of the node.
          //Postcondition: The value of link is returned.

      nodeType();
          //Default constructor
          //Postcondition: link = NULL;

      nodeType(const Type& elem, nodeType<Type> *ptr);
          //Constructor with parameters
          //Sets info to point to the object elem points to, and
          //link is set to point to the object ptr points to.
          //Postcondition: info = elem; link = ptr

      nodeType(const nodeType<Type> &otherNode);
          //Copy constructor
      ~nodeType();
          //Destructor

  private:
      Type info;
      nodeType<Type> *link;
  };
  ```

  Write the definitions of the member functions of the class `nodeType`. Also, write a program to test your class.

- 10. Programming Exercise 9 asks you to redefine the class to implement the nodes of a linked list so that the instance variables are private. Therefore, the class `linkedListType` and its derived classes `unorderedLinkedList` and `orderedLinkedList` can no longer directly access the instance variables of the class `nodeType`. Rewrite the definitions of these classes so that they use the member functions of the class `nodeType` to access the info and link fields of a node. Also, write programs to test various operations of the classes `unorderedLinkedList` and `orderedLinkedList`.

- 11. Write the definitions of the function `copyList`, the copy constructor, and the function to overload the assignment operator for the class `doublyLinkedList`.

- 12. Write a program to test various operations of the class `doublyLinkedList`.

- 13. **(Circular linked lists)** This chapter defined and identified various operations on a circular linked list.
  - a. Write the definitions of the class `circularLinkedList` and its member functions. (You may assume that the elements of the circular linked list are in ascending order.)
  - b. Write a program to test various operations of the class defined in (a).

- 14. **(Video Store programming example)**
  - a. Complete the design and implementation of the class `customerType` defined in the Video Store programming example.
  - b. Design and implement the class `customerListType` to create and maintain a list of customers for the video store.

- 15. **(Video Store programming example)** Complete the design and implementation of the video store program. In other words, write a program that uses the classes designed in the Video Store programming example and in Programming Exercise 14 to make a video store operational.
