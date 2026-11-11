
In Figure 13, the r and p are the pointer variables that contain the address of a node. You can also see that first of all, the program contains the address of the first node (in r and p) of the linked list. The last element of the first node contains the address of the next node. In the second node, the last element of the node contains NULL, which specifies the end of the linked list.

One more thing to remember about a linked list data structure is that it generally stores the values in LIFO (Last In First Out) memory allocation. This implies that the values stored at last are accessed first and vice versa.

Listing 12 shows a complete code of creating and displaying elements of a linked list (you can find the LinkList.cpp file on the CD in the `code\chapter5` folder):

## ▶ Listing 12: Creating and Displaying a Linked List

```cpp
#include<iostream.h>
struct node                              //a structure is declared
{
        int qty ;                         //data1
        int price;                        //data2
        struct node *next;                //pointer to next element
}*p;                                      //global pointer to denote first node
void addnode(int q , int pr)
{
        struct node *temp = new node;     //allocate memory for the new node
        temp->qty = q ;                   //set data field-1
        temp->price = pr;                 //set data field-2
        if(p==NULL)                       //if no list is currently available
        {
                p = temp;                 //new node points to the first node
                p->next = NULL;           //set next address field
        }
        else
        {
                temp->next = p;
                p = temp;                 //p now points to the new node
        }
}
void display(struct node &r)
{
        r = p;
        // assign the address stored in p to r.
        // set pointer to the current element
        if(r == NULL)                     //if no list is at current position
        {
                cout<<"no list";
                return;
        }

        while(r!=NULL)                    //traverse through whole list until address field is null
        {
```

The display() function is called from the main() function to display all the items of each node to the user.

## TEST YOUR KNOWLEDGE

### Q9. Create a program that displays the details of the persons currently stored in the list. It should also allow the user to add details of more persons and delete details of existing persons either from the beginning or from the end.

Ans.

```cpp
#include <iostream.h>
struct PersonDetails
{  char name[20];
   int age;
   float height;
   PersonDetails *next_nd;
};

PersonDetails *start_ptr = NULL;
PersonDetails *current;
int option = 0;
void AddDetailsEnd()
{  PersonDetails *temp, *temp2;

   // Reserve space for new PersonDetails and fill it with data
   temp = new PersonDetails;
   cout << "Please enter the name of the person: ";
   cin >> temp->name;
   cout << "Please enter the age of the person : ";
   cin >> temp->age;
   cout << "Please enter the height of the person : ";
   cin >> temp->height;
   temp->next_nd = NULL;

   // Set up link to this PersonDetails
   if (start_ptr == NULL)
   {  start_ptr = temp;
      current = start_ptr;
   }
   else
   {  temp2 = start_ptr;
      // We know this is not NULL - list not empty!
      while (temp2->next_nd != NULL)
      {  temp2 = temp2->next_nd;
         // Move to next link in chain
      }
      temp2->next_nd = temp;
   }
}
void DisplayDetails()
{
    PersonDetails *temp;
    temp = start_ptr;
    cout << endl;
    if (temp == NULL)
        cout << "The list is empty!" << endl;
    else
    {
        while (temp != NULL)
        {
            // Display details for what temp points to
            cout << "Name : " << temp->name << ";";
            cout << "Age : " << temp->age << ";";
            cout << "Height : " << temp->height;
            if (temp == current)
            {
                cout << " <-- Current PersonDetails";
                cout << endl;
                temp = temp->next_nd;
            }
        }
        cout << "End of list!" << endl;
    }
}
void DeletePersonDetailsStart()
{
    PersonDetails *temp;
    temp = start_ptr;
    start_ptr = start_ptr->next_nd;
    delete temp;
}
void DeletePersonDetailsEnd()
{
    PersonDetails *temp1, *temp2;
    if (start_ptr == NULL)
        cout << "The list is empty!" << endl;
    else
    {
        temp1 = start_ptr;
        if (temp1->next_nd == NULL)
        {
            delete temp1;
            start_ptr = NULL;
        }
        else
        {
            while (temp1->next_nd != NULL)
            {
                temp2 = temp1;
                temp1 = temp1->next_nd;
            }
            delete temp1;
            temp2->next_nd = NULL;
        }
    }
}
void main()
{
    clrscr();
    start_ptr = NULL;
    do
    {
        DisplayDetails();
        cout << endl;
        cout << "Please select an option : " << endl;
        cout << "0. Exit the program." << endl;
        cout << "1. Add a person details to the end of the list." << endl;
        cout << "2. Delete a person details from the beginning of the list." << endl;
        cout << "3. Delete a person details from the end of the list." << endl;

        cout << endl << ">> ";
        cin >> option;

        switch (option)
        {
            case 1 : AddDetailsEnd(); break;
            case 2 : DeletePersonDetailsStart(); break;
            case 3 : DeletePersonDetailsEnd();
        }
    }
    while (option != 0);
}
```

### Output:

```text
The list is empty!

Please select an option :
0. Exit the program.
1. Add a person details to the end of the list.
2. Delete a person details from the beginning of the list.
3. Delete a person details from the end of the list.

>> 1
Please enter the name of the person: Dheeraj
Please enter the age of the person : 23
Please enter the height of the person : 6
Name : Dheeraj;Age : 23;Height : 6 <-- Current PersonDetails
End of list!

Please select an option :
0. Exit the program.
1. Add a person details to the end of the list.
2. Delete a person details from the beginning of the list.
3. Delete a person details from the end of the list.

>>
```

### Q10. Create a program that accepts details of a flat (Builder name, number of rooms, price) and displays them on the screen. This program must use a structure to store all the flat details and a function that takes pointer of that structure to accept and display the flat details.

Ans.

```cpp
#include <iostream.h>
#include <stdio.h>

struct flat
{
    char name[30];
    int rooms;
    int price;
};

void func(flat *new_flat)
{
    cout<<"Enter Builder name: ";
    gets(new_flat->name);
    cout<<"Enter number of Rooms in the Flat: ";
    cin>>new_flat->rooms;
    cout<<"Enter Price in Lakhs: ";
    cin>>new_flat->price;
    cout<<"The description of the flat is -->"<<endl;
    cout<<"--------------------------------"<<endl;
    cout<<"Builder Name: "<<new_flat->name<<endl;
    cout<<"Number of Rooms: "<<new_flat->rooms<<endl;
    cout<<"Price of flat in Lakhs: "<<new_flat->price<<endl;
}

int main()
{
    flat f1, *new_flat;
    new_flat = &f1;
    func(new_flat);
    return 0;
}
```

### Output:

```text
Enter Builder name: Parsvanath

Enter number of Rooms in the Flat: 5
Enter Price in Lakhs: 35
The description of the flat is -->
-----------------------------------
Builder Name: Parsvanath
Number of Rooms: 5
Price of flat in Lakhs: 35
```

Now, you are familiar with structures, let's move on to learn union in C++.

## 5.2 Union in C++

Similar to structures, unions are also user-defined data types. They contain elements of different data types. Unlike structures, the members of a particular union can share the same storage area within the computer’s memory. Unions are useful for applications that involve multiple members and where the values need not be assigned to all the members at the same time. The syntax to define a union is as follows:

```cpp
union <unionname>
{
member1;
member2;
.
.
};
```

In the preceding syntax, you see that the declaration of a union starts with the keyword `union`, followed by a user-defined union name, and then curly braces. Within the body (between opening and closing curly braces) of a union, you can define any number of members or variables of any data type, such as `int`, `float`. An example to define a union is shown in the following code snippet:

```cpp
union number
{
    int intvalue;
    long longvalue;
    double doublevalue;
};
```

Let’s now explain the difference between a union and a structure with the help of an example. Consider the following code snippet, in which a structure `user_var` is defined:

```cpp
struct user_var
{
    float f;
    char ch[4];
} s1;
```
