
- 3. To check in a DVD
- 4. To check whether a particular DVD is in stock
- 5. To print only the titles of all the DVDs
- 6. To print a list of all the DVDs
- 7. To exit

In pseudocode, Step 4 (of the main program) is:

```text
a. get choice
b.
    while (choice != 9)
    {
        switch (choice)
        {
        case 1:
            a. get the movie name
            b. search the DVD list
            c. if found, report success
                else report "failure"
            break;
        case 2:
            a. get the movie name
            b. search the DVD list
            c. if found, check out the DVD
                else report "failure"
            break;
        case 3:
            a. get the movie name
            b. search the DVD list
            c. if found, check in DVD
                else report "failure"
            break;
        case 4:
            a. get the movie name
            b. search the DVD list
            c. if found, check whether the DVD is in stock
                if number of copies > 0
                    report "success"
                else
                    report "currently out of stock"
            else report "failure"
            break;
        case 5:
            print the titles of the DVDs
            break;
        case 6:
            print all the DVDs in the store
            break;
        default: invalid selection
        } //end switch
        displayMenu();
        get choice;
    }//end while
```

### PROGRAM LISTING

```cpp
/********************************************************************
 // Author: D.S. Malik
 //
 // This program uses the classes dvdType and dvdListType to
 // create a list of DVDs for a DVD store. It also performs
 // basic operations such as find and check out DVDs.
 //********************************************************************

#include <iostream>
#include <fstream>
#include <string>
#include "dvdType.h"
#include "dvdListType.h"

using namespace std;

void createDVDList(ifstream& infile,
                   dvdListType& dvdList);
void displayMenu();

int main()
{
    dvdListType dvdList;
    int choice;
    char ch;
    string title;

    ifstream infile;

        //open the input file
    infile.open("dvdDat.txt");
    if (!infile)
    {
        cout << "The input file does not exist. "
             << "The program terminates!!!" << endl;
        return 1;
    }

        //create the DVD list
    createDVDList(infile, dvdList);
    infile.close();

        //show the menu
    displayMenu();
    cout << "Enter your choice: ";
    cin >> choice;       //get the request
    cin.get(ch);
    cout << endl;

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

        displayMenu();    //display menu

        cout << "Enter your choice: ";
        cin >> choice;    //get the next request
        cin.get(ch);
        cout << endl;
    }//end while

    return 0;

}

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
    }//end while
}//end createDVDList

void displayMenu()
{
    cout << "Select one of the following:" << endl;
    cout << "1: To check whether the store carries a "
         << "particular DVD." << endl;
    cout << "2: To check out a DVD." << endl;
    cout << "3: To check in a DVD." << endl;
    cout << "4: To know whether a particular DVD is "
         << "in stock." << endl;
    cout << "5: To print only the titles of all the DVDs."
         << endl;
    cout << "6: To print a list of all the DVDs." << endl;
    cout << "9: To exit" << endl;
}//end displayMenu
```

### QUICK REVIEW

- 1. A linked list is a list of items, called nodes, in which the order of the nodes is determined by the address, called a link, stored in each node.
- 2. The pointer to a linked list—that is, the pointer to the first node in the list—is stored in a separate location called the **head** or **first**.
- 3. A linked list is a dynamic data structure.
- 4. The length of a linked list is the number of nodes in the list.
- 5. Item insertion and deletion from a linked list do not require data movement; only the pointers are adjusted.
- 6. A (single) linked list is traversed in only one direction.
- 7. The search on a linked list is sequential.
- 8. The first (or head) pointer of a linked list is always fixed, pointing to the first node in the list.
- 9. To traverse a linked list, the program must use a pointer different than the head pointer of the list, initialized to the first node in the list.
- 10. In a doubly linked list, every node has two links: one points to the next node and one points to the previous node.
- 11. A doubly linked list can be traversed in either direction.
- 12. In a doubly linked list, item insertion and deletion require the adjustment of two pointers in a node.
- 13. A linked list in which the last node points to the first node is called a circular linked list.

### EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

- 1. Mark the following statements as true or false.
  - a. Every node in a linked list has two components: one to store the relevant information and one to store the address. (1)
  - b. In a linked list, the order of the elements is determined by the order in which the nodes were created to store the elements. (1)
  - c. In a linked list, memory allocated for the nodes is sequential. (1, 2)
  - d. In a linked list, typically, the link field of the last node points to itself. (1, 2)
  - e. Suppose the nodes of a linked list are in the usual info-link form and current points to a node of the linked list. Then current = current.link; advances current to the next node in the linked list. (2)
  - f. To insert a new item in a linked list, create a node, store the new item in the node, and insert the node in the linked list. (3)
  - g. To build a linked list forward, the new node is inserted at the end of the list. (4)
