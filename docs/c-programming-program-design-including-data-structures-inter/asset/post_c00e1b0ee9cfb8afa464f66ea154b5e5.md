
template. Because we are now dealing with a very specific data type, the class `dvdListType` is no longer required to be a template. Thus, the info type of each node in the linked list is now `dvdType`. Through the member functions of the class `dvdType`, certain members—such as `dvdTitle` and `copiesInStock` of an object of type `dvdType`—can now be accessed.

The definitions of the functions to implement the operations of the class `dvdListType` are given next.

The primary operations on the DVD list are to check in a DVD and to check out a DVD. Both operations require the list to be searched and the location of the DVD being checked in or checked out to be found in the DVD list. Other operations, such as determining whether a particular DVD is in the store, updating the number of copies of a DVD, and so on, also require the list to be searched. To simplify the search process, we will write a function that searches the DVD list for a particular DVD. If the DVD is found, it sets a parameter `found` to true and returns a pointer to the DVD so that check-in, check-out, and other operations on the DVD object can be performed. Note that the function `searchDVDList` is a private data member of the class `dvdListType` because it is used only for internal manipulation. First, we describe the search procedure.

Consider the node of the DVD list shown in Figure 16-47.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1143_0.png)

The component `info` is of type `dvdType` and contains the necessary information about a DVD. In fact, the component `info` of the node has seven members: `dvdTitle`, `movieStar1`, `movieStar2`, `movieProducer`, `movieDirector`, `movieProductionCo`, and `copiesInStock`. (See the definition of the class `dvdType`.) Therefore, the node of a DVD list has the form shown in Figure 16-48.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1144_0.png)

**FIGURE 16-48** DVD list node showing components of *info*

These member variables are all private and cannot be accessed directly. The member functions of the class `dvdType` will help us in checking and/or setting the value of a particular component.

Suppose a pointer—say, `current`—points to a node in the DVD list (see Figure 16-49).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1144_1.png)

**FIGURE 16-49** Pointer `current` and DVD list node

Now:

```
current->info
```

refers to the info part of the node. Suppose that we want to know whether the title of the DVD stored in this node is the same as the title specified by the variable title. The expression:

```
current->info.checkTitle(title)
```

is true if the title of the DVD stored in this node is the same as the title specified by the parameter title, and false otherwise. (Note that the member function checkTitle is a value-returning function. See its declaration in the class dvdType.)

As another example, suppose that we want to set copiesInStock of this node to 10. Because copiesInStock is a private member, it cannot be accessed directly. Therefore, the statement:

```
current->info.copiesInStock = 10;   //illegal
```

is incorrect and will generate a compile-time error. We have to use the member function setCopiesInStock as follows:

```
current->info.setCopiesInStock(10);
```

Now that we know how to access a member variable of a DVD stored in a node, let us describe the algorithm to search the DVD list.

```
while (not found)
    if the title of the current DVD is the same as the desired
        title, stop the search
    else
        check the next node
```

The following function definition performs the desired search:

```cpp
void dvdListType::searchDVDList(string title, bool& found,
                                nodeType<dvdType>*& current) const
{
    found = false;    //set found to false

    current = first; //set current to point to the first node
                     //in the list

    while (current != NULL && !found)    //search the list
        if (current->info.checkTitle(title)) //the item is found
            found = true;
        else
            current = current->link; //advance current to
                                      //the next node
} //end searchDVDList
```

If the search is successful, the parameter found is set to true and the parameter current points to the node containing the DVD info. If it is unsuccessful, found is set to false and current will be NULL.

The definitions of the other functions of the class dvdListType follow:

```cpp
bool dvdListType::isDVDAvailable(string title) const
{
    bool found;
    nodeType<dvdType> * location;

    searchDVDList(title, found, location);

    if (found)
        found = (location->info.getNoOfCopiesInStock() > 0);
    else
        found = false;

    return found;
}

void dvdListType::dvdCheckIn(string title)
{
    bool found = false;
    nodeType<dvdType> * location;

    searchDVDList(title, found, location); //search the list

    if (found)
        location->info.checkIn();
    else
        cout << "The store does not carry " << title
             << endl;
}

void dvdListType::dvdCheckOut(string title)
{
    bool found = false;
    nodeType<dvdType> * location;

    searchDVDList(title, found, location); //search the list

    if (found)
        location->info.checkOut();
    else
        cout << "The store does not carry " << title
             << endl;
}
```

```cpp
bool dvdListType::dvdCheckTitle(string title) const
{
    bool found = false;
    nodeType<dvdType> *location;

    searchDVDList(title, found, location); //search the list

    return found;
}

void dvdListType::dvdUpdateInStock(string title, int num)
{
    bool found = false;
    nodeType<dvdType> *location;

    searchDVDList(title, found, location); //search the list

    if (found)
        location->info.updateInStock(num);
    else
        cout << "The store does not carry " << title
             << endl;
}

void dvdListType::dvdSetCopiesInStock(string title, int num)
{
    bool found = false;
    nodeType<dvdType> *location;

    searchDVDList(title, found, location);

    if (found)
        location->info.setCopiesInStock(num);
    else
        cout << "The store does not carry " << title
             << endl;
}

bool dvdListType::dvdSearch(string title) const
{
    bool found = false;
    nodeType<dvdType> *location;

    searchDVDList(title, found, location);

    return found;
}
```

```cpp
void dvdListType::dvdPrintTitle() const
{
    nodeType<dvdType>* current;

    current = first;
    while (current != NULL)
    {
        current->info.printTitle();
        current = current->link;
    }
}
```

## Customer Object

The customer object stores information about a customer, such as the first name, last name, account number, and a list of DVDs rented by the customer.

Every customer is a person. We have already designed the class personType in Example 11-10 (Chapter 10) and described the necessary operations on the name of a person. Therefore, we can derive the class customerType from the class personType and add the additional members that we need. First, however, we must redefine the class personType to take advantage of the new features of object-oriented design that you have learned, such as operator overloading, and then derive the class customerType.

Recall that the basic operations on an object of type personType are:

- 1. Print the name.
- 2. Set the name.
- 3. Show the first name.
- 4. Show the last name.

Similarly, the basic operations on an object of type customerType are:

- 1. Print the name, account number, and the list of rented DVDs.
- 2. Set the name and the account number.
- 3. Rent a DVD; that is, add the rented DVD to the list.
- 4. Return a DVD; that is, delete the rented DVD from the list.
- 5. Show the account number.

The details of implementing the customer component are left as an exercise for you. (See Programming Exercise 14 at the end of this chapter.)

## Main Program

We will now write the main program to test the DVD object. We assume that the necessary data for the DVDs are stored in a file. We will open the file and create the
