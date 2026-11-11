display() function is called from the main() function to display all the items of each node to the user.

# TEST YOUR KNOWLEDGE

Q9. Create a program that displays the details of the persons currently stored in the list. It should also allow the user to add details of more persons and delete details of existing persons either from the beginning or from the end.

Ans.

```
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
```
```