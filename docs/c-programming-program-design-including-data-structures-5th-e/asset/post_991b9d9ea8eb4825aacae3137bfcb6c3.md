
```cpp
void createVideoList(ifstream& infile,
                     videoListType& videoList)
{
    string title;
    string star1;
    string star2;
    string producer;
    string director;
    string productionCo;

    char ch;
    int inStock;

    videoType newVideo;

    getline(infile, title);

    while (infile)
    {
        getline(infile, star1);
        getline(infile, star2);
        getline(infile, producer);
        getline(infile, director);
        getline(infile, productionCo);
        infile >> inStock;
        infile.get(ch);
        newVideo.setVideoInfo(title, star1, star2, producer,
                              director, productionCo, inStock);

        videoList.insertFirst(newVideo);

        getline(infile, title);
    }//end while
}//end createVideoList

void displayMenu()
{
    cout << "Select one of the following:" << endl;
    cout << "1: To check whether the store carries a "
         << "particular video." << endl;
    cout << "2: To check out a video." << endl;
    cout << "3: To check in a video." << endl;
    cout << "4: To check whether a particular video is "
         << "in stock." << endl;
    cout << "5: To print only the titles of all the videos."
         << endl;
    cout << "6: To print a list of all the videos." << endl;
    cout << "9: To exit" << endl;
}//end displayMenu
```

## QUICK REVIEW

- 1. A linked list is a list of items, called nodes, in which the order of the nodes is determined by the address, called a link, stored in each node.
- 2. The pointer to a linked list—that is, the pointer to the first node in the list—is stored in a separate location called the head or first.
- 3. A linked list is a dynamic data structure.
- 4. The length of a linked list is the number of nodes in the list.
- 5. Item insertion and deletion from a linked list do not require data movement; only the pointers are adjusted.
- 6. A (single) linked list is traversed in only one direction.
- 7. The search on a linked list is sequential.
- 8. The first (or head) pointer of a linked list is always fixed, pointing to the first node in the list.
- 9. To traverse a linked list, the program must use a pointer different than the head pointer of the list, initialized to the first node in the list.
- 10. In a doubly linked list, every node has two links: one points to the next node, and one points to the previous node.
- 11. A doubly linked list can be traversed in either direction.
- 12. In a doubly linked list, item insertion and deletion require the adjustment of two pointers in a node.
- 13. A linked list in which the last node points to the first node is called a circular linked list.

## EXERCISES

- 1. Mark the following statements as true or false.
  - a. In a linked list, the order of the elements is determined by the order in which the nodes were created to store the elements.
  - b. In a linked list, memory allocated for the nodes is sequential.
  - c. A single linked list can be traversed in either direction.
  - d. In a linked list, nodes are always inserted either at the beginning or the end because a linked list is not a random-access data structure.
- 2. Describe the two typical components of a single linked list node.
- 3. What is stored in the link field of the last node of a nonempty single linked list?
- 4. Suppose that first is a pointer to a linked list. What is stored in first?
- 5. Suppose that the fourth node of a linked list is to be deleted, and p points to the fourth node. Why do you need a pointer to the third node of the linked list?

Consider the linked list shown in Figure 17-50. Assume that the nodes are in the usual info-link form. Use this list to answer Exercises 6 through 12. If necessary, declare additional variables. (Assume that list, p, s, A, and B are pointers of type `nodeType`.)

![](img/f97f778697507bb6fdd80c5991210cba_1114_0.png)

**FIGURE 17-50** Linked list for exercises 6 through 12

- 6. What is the output of each of the following C++ statements?
  - a. `cout << list->info;`
  - b. `cout << A->info;`
  - c. `cout << B->link->info;`
  - d. `cout << list->link->link->info;`
- 7. What is the value of each of the following relational expressions?
  - a. `list->info >= 18`
  - b. `list->link == A`
  - c. `A->link->info == 16`
  - d. `B->link == NULL`
  - e. `list->info == 18`
- 8. Mark each of the following statements as valid or invalid. If a statement is invalid, explain why.
  - a. `A = B;`
  - b. `list->link = A->link;`
  - c. `list->link->info = 45;`
  - d. `*list = B;`
  - e. `*A = *B;`
  - f. `B = A->link->info;`
  - g. `A->info = B->info;`
  - h. `list = B->link->link;`
  - i. `B = B->link->link->link;`

- 9. Write C++ statements to do the following.
  - a. Make A point to the node containing info 23.
  - b. Make list point to the node containing 16.
  - c. Make B point to the last node in the list.
  - d. Make list point to an empty list.
  - e. Set the value of the node containing 25 to 35.
  - f. Create and insert the node with info 10 after the node pointed to by A.
  - g. Delete the node with info 23. Also, deallocate the memory occupied by this node.

- 10. What is the output of the following C++ code?

```cpp
p = list;

while (p != NULL)
    cout << p->info << " ";
    p = p->link;
cout << endl;
```

- 11. If the following C++ code is valid, show the output. If it is invalid, explain why.

```cpp
s = A;
p = B;
s->info = B;
p = p->link;
cout << s->info << " " << p->info << endl;
```

- 12. If the following C++ code is valid, show the output. If it is invalid, explain why.

```cpp
p = A;
p = p->link;
s = p;
p->link = NULL;
s = s->link;
cout << p->info << " " << s->info << endl;
```

- 13. Show what is produced by the following C++ code. Assume the node is in the usual info-link form with the info of type int. (list and ptr are pointers of type nodeType.)

```cpp
list = new nodeType;
list->info = 10;
ptr = new nodeType;
ptr->info = 13;
ptr->link = NULL;
list->link = ptr;
ptr = new nodeType;
ptr->info = 18;
ptr->link = list->link;
list->link = ptr;
cout << list->info << " " << ptr->info << " ";
ptr = ptr->link;
cout << ptr->info << endl;
```

- 14. Show what is produced by the following C++ code. Assume the node is in the usual info-link form with the info of type `int`. (list and ptr are pointers of type nodeType.)

```cpp
list = new nodeType;
list->info = 20;
ptr = new nodeType;
ptr->info = 28;
ptr->link = NULL;
list->link = ptr;
ptr = new nodeType;
ptr->info = 30;
ptr->link = list;
list = ptr;
ptr = new nodeType;
ptr->info = 42;
ptr->link = list->link;
list->link = ptr;
ptr = list;
while (ptr != NULL)
{
    cout << ptr->info << endl;
    ptr = ptr->link;
}
```

- 15. Assume that the node of a linked list is in the usual info-link form with the info of type `int`. The following data, as described in parts (a) to (d), is to be inserted into an initially empty linked list: 72, 43, 8, 12. Suppose that head is a pointer of type nodeType. After the linked list is created, head should point to the first node of the list. Declare additional variables as you need them. Write the C++ code to create the linked list. After the linked list is created, write a code to print the list. What is the output of your code?
  - a. Insert 72 into an empty linked list.
  - b. Insert 43 before 72.
  - c. Insert 8 at the end of the list.
  - d. Insert 12 after 43.

- 16. Assume that the node of a linked list is in the usual info-link form with the info of type `int`. (list and ptr are pointers of type nodeType.) The following code creates a linked list.

```cpp
ptr = new nodeType;
ptr->info = 16;
list = new nodeType;
list->info = 25;
list->link = ptr;
ptr = new nodeType;
ptr->info = 12;
ptr->link = NULL;
list->link->link = ptr;
```

Use the linked list created by this code to answer the following questions. (These questions are independent of each other.) Declare additional pointers if you need them.

  - a. Which pointer points to the first node of the linked list?
  - b. Determine the order of the nodes of the linked list.
  - c. Write a C++ code that creates and inserts a node with info 45 after the node with info 16.
  - d. Write a C++ code that creates and inserts a node with info 58 before the node with info 25. Does this require you to change the value of the pointer that was pointing to the first node of the linked list?
  - e. Write a C++ code that deletes the node with info 25. Does this require you to change the value of the pointer that was pointing to the first node of the linked list?

- 17. Consider the following C++ statements. (The class `unorderedLinkedList` is as defined in this chapter.)

```cpp
unorderedLinkedList<int> list;

list.insertFirst(15);
list.insertLast(28);
list.insertFirst(30);
list.insertFirst(2);
list.insertLast(45);
list.insertFirst(38);
list.insertFirst(25);
list.deleteNode(30);
list.insertFirst(18);
list.deleteNode(28);
list.deleteNode(12);
list.print();
```

What is the output of this program segment?

- 18. Suppose the input is:

`18 30 4 32 45 36 78 19 48 75 -999`

What is the output of the following C++ code? (The class `unorderedLinkedList` is as defined in this chapter.)

```cpp
unorderedLinkedList<int> list;
unorderedLinkedList<int> copyList;
int num;

cin >> num;
while (num != -999)
```
