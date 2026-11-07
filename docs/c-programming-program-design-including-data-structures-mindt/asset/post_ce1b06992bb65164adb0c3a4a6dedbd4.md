
```cpp
//process the requests
while (choice != 9)
{
    switch (choice)
    {
    case 1:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
            cout << "The store carries " << title
                 << endl;
        else
            cout << "The store does not carry "
                 << title << endl;
        break;

    case 2:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
        {
            if (dvdList.isDVDAvailable(title))
            {
                dvdList.dvdCheckOut(title);
                cout << "Enjoy your movie: "
                     << title << endl;
            }
            else
                cout << "Currently " << title
                     << " is out of stock." << endl;
        }
        else
            cout << "The store does not carry "
                 << title << endl;
        break;

    case 3:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
        {
            dvdList.dvdCheckIn(title);
            cout << "Thanks for returning "
                 << title << endl;
        }
        else
            cout << "The store does not carry "
                 << title << endl;
        break;

    case 4:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
        {
            if (dvdList.isDVDAvailable(title))
                cout << title << " is currently in "
                     << "stock." << endl;
            else
                cout << title << " is currently out "
                     << "of stock." << endl;
        }
        else
            cout << "The store does not carry "
                 << title << endl;
        break;

    case 5:
        dvdList.dvdPrintTitle();
        break;

    case 6:
        dvdList.print();
        break;

    default:
        cout << "Invalid selection." << endl;
    }//end switch

    displayMenu();   //display menu

    cout << "Enter your choice: ";
    cin >> choice;   //get the next request
    cin.get(ch);
    cout << endl;
}//end while

return 0;
}
```

```cpp
void createDVDList(ifstream& infile,
                   dvdListType& dvdList)
{
    string title;
    string star1;
    string star2;
    string producer;
    string director;
    string productionCo;
    char ch;
    int inStock;

    dvdType newDVD;

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
        newDVD.setDVDInfo(title, star1, star2, producer,
                          director, productionCo, inStock);

        dvdList.insertFirst(newDVD);

        getline(infile, title);
    } //end while
} //end createDVDList

void displayMenu()
{
    cout << "Select one of the following:" << endl;
    cout << "1: To check whether the store carries a "
         << "particular DVD." << endl;
    cout << "2: To check out a DVD." << endl;
    cout << "3: To check in a DVD." << endl;
    cout << "4: To check whether a particular DVD is "
         << "in stock." << endl;
    cout << "5: To print only the titles of all the DVDs."
         << endl;
    cout << "6: To print a list of all the DVDs." << endl;
    cout << "9: To exit" << endl;
} //end displayMenu
```

## QUICK REVIEW

1. A linked list is a list of items, called nodes, in which the order of the nodes is determined by the address, called a link, stored in each node.
2. The pointer to a linked list—that is, the pointer to the first node in the list—is stored in a separate location called the head or first.
3. A linked list is a dynamic data structure.
4. The length of a linked list is the number of nodes in the list.
5. Item insertion and deletion from a linked list do not require data movement; only the pointers are adjusted.
6. A (single) linked list is traversed in only one direction.
7. The search on a linked list is sequential.
8. The first (or head) pointer of a linked list is always fixed, pointing to the first node in the list.
9. To traverse a linked list, the program must use a pointer different than the head pointer of the list, initialized to the first node in the list.
10. In a doubly linked list, every node has two links: one points to the next node and one points to the previous node.
11. A doubly linked list can be traversed in either direction.
12. In a doubly linked list, item insertion and deletion require the adjustment of two pointers in a node.
13. A linked list in which the last node points to the first node is called a circular linked list.

## EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

1. Mark the following statements as true or false.
   a. Every node in a linked list has two components: one to store the relevant information and one to store the address. (1)
   b. In a linked list, the order of the elements is determined by the order in which the nodes were created to store the elements. (1)
   c. In a linked list, memory allocated for the nodes is sequential. (1, 2)
   d. In a linked list, typically, the link field of the last node points to itself. (1, 2)
   e. Suppose the nodes of a linked list are in the usual info-link form and `current` points to a node of the linked list. Then `current = current.link;` advances `current` to the next node in the linked list. (2)
   f. To insert a new item in a linked list, create a node, store the new item in the node, and insert the node in the linked list. (3)
   g. To build a linked list forward, the new node is inserted at the end of the list. (4)
   h. A single linked list can be traversed in either direction. (2, 4, 5)
   i. In a linked list, nodes are always inserted either at the beginning or at the end because a linked list is not a random-access data structure. (4, 5, 8, 9)
   j. The head pointer of a linked list should not be used to traverse the list. (2, 4, 7)
   k. The two most common operations on iterators are ++ and * (the dereferencing operator). (6)
   l. The function `initializeList` of the class `linkedListType` initializes the list by only setting the pointers `first` and `last` to `nullptr`. (7)
   m. The function `search` of the class `unorderedLinkedList` searches the linked list sequentially, while the function `search` of the class `orderedLinkedList` searches the list using a binary search algorithm because the data in an `orderedLinkedList` object is sorted. (8, 9)
   n. A doubly linked list can be traversed in either direction. (10)

2. Describe the two typical components of a single linked list node. (1)

3. What is stored in the link field of the last node of a nonempty single linked list? (2)

4. Suppose that `first` is a pointer to a linked list. What is stored in `first`? (2)

5. Suppose that the fourth node of a linked list is to be deleted, and `p` points to the fourth node? Why do you need a pointer to the third node of the linked list? (3)

Consider the linked list and the variable declaration shown in Figure 16-50, where `nodeType` is a `struct` with two components: `info` of type `int` and `link` of type `nodeType`. Use this list to answer Exercises 6 through 14.

![](img/b217c421655b51e7494cf3b89bb5432d_1216_0.png)

FIGURE 16-50  Linked list for Exercises 6–14.

6. What is the output, if any, of each of the following C++ statements? (For each part, use the same list in Figure 16-50.) (3, 4)

```cpp
a. cout << p->info;

b. q = p->link;
   cout << q->info << " " << current->info;

c. cout << current->link->info;

d. trail = current->link->link;
   trail->link = nullptr;
   cout << trail->info;

e. cout << last->link->info;

f. q = current->link;
   cout << q->link->link->info;
```

7. What is the value of each of the following relational expressions? (3, 4)
   a. `p->link->link == current`
   b. `first->link->link->info == 92`
   c. `temp->link == 0`
   d. `last->link == nullptr`
   e. `list->link == p`
   f. `p->link->link->link->info == temp->info`

8. What are the effects, if any, of each of the following C++ statements? (3, 4)

```cpp
a. trail = temp->link;
   trail->link = nullptr;
   delete last;
   last = trail;

b. temp->link = last;

c. first->info = 58;

d. q = current->link;
   current->link = temp;
   delete q;

e. q = p->link->link->link;
   q->info = 60;

f. p->link = temp;
```

9. Write C++ statements to do the following. (3, 4)
   a. Set the info of the third node to 24.
   b. Make q point to the node with info 80.
