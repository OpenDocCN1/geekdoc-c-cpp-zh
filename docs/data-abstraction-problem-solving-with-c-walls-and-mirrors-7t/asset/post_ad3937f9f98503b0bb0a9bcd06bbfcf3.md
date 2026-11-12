
```
{
   if (curPtr != nullPtr)
   {
      bagContents.push_back(curPtr->getItem());
      fillVector(bagContents, curPtr->getNext());
   } // end if
} // end fillVector
```

Even though fillVector has a reference parameter, the method is safe because it is private. A similar situation occurs in Chapter 16 and is discussed further in a Note in Section 16.3.1.

### The private method getPointerTo.

The method getPointerTo locates a given entry within the linked chain. To do so, it traverses the linked chain, but unlike fillVector's traversal, this traversal stops if it locates the node that contains the given entry. The iterative version of getPointerTo has one parameter, which is the given entry. We could define a private method to perform the recursion—as we did for toVector—that has two parameters: the given entry and a head pointer. Then getPointerTo could call this new private method. However, since getPointerTo is itself a private method, we can revise it to have the necessary two parameters. That is the approach we will take here. Of course, we also will have to revise the calls to the method that appear in the rest of the class.

We begin by replacing the declaration of getPointerTo in the header file for the class LinkedBag with the following statements:

```
// Locates a given entry within this bag.
// Returns either a pointer to the node containing a given entry or
// the null pointer if the entry is not in the bag.
Node<ItemType>* getPointerTo(const ItemType& target,
Node<ItemType>* curPtr) const;
```

Before we forget to do so, let's revise the calls to this method that occur in the methods remove and contains. The original calls are getPointerTo(anEntry), but they now each need to be getPointerTo(anEntry, headPtr).

The recursive definition of this method has two base cases. One case occurs when the chain is empty, causing the method to return nullPtr. The other base case occurs when we locate the desired entry at curPtr->getItem(). In this case, the method returns curPtr. The recursive step searches the chain beginning at curPtr->getNext(). Thus, the method has the following definition:

```
template<class ItemType>
Node<ItemType>* getPointerTo(const ItemType& target,
Node<ItemType>* curPtr) const
{
   Node<ItemType>* result = nullptr;
   if (curPtr != nullptr)
   {
      if (target == curPtr->getItem())
         result = curPtr;
      else
         result = getPointerTo(target, curPtr->getNext());
   } // end if
   return result;
} // end getPointerTo
```

Other methods that can have a recursive definition are left for you as exercises.

### Question 14

Revise the method clear so that it calls a recursive method to deallocate the nodes in the chain.

## 4.4 Testing Multiple ADT Implementations

In Chapter 3, we developed a short program, shown in Listing 3-2, that tested the core methods of our array-based bag implementation. Because we used ADT bag methods when we tested our implementation, we can use the same code—with a few changes—to test our linked implementation. You need only to change each occurrence of ArrayBag to LinkedBag and recompile the program.

But what if later you change the array-based implementation and want to retest it? You would need to change each occurrence of LinkedBag back to ArrayBag. Let’s examine a way we can revise the test program to let the user decide which bag implementation needs testing. By taking advantage of polymorphism, we can do this without needing to duplicate the test code.

In Chapter 1, we described our ADT bag in the abstract class BagInterface. Since both ArrayBag and LinkedBag share public methods defined in that class, we made each a subclass of BagInterface. In our test program, if we declare the variable bagPtr as a pointer to an object that implements the methods in BagInterface, we can use an instance of either ArrayBag or LinkedBag as the object bagPtr references. We declare bagPtr as

```
BagInterface<string>* bagPtr;
```

We then ask the user which implementation to test, and if we assign either 'A' or 'L' to the char variable userChoice, we can instantiate an instance of the requested bag type and run the test by writing the following code:

```
if (userChoice == 'A')
{
    bagPtr = new ArrayBag<string>();
    cout << "Testing the Array-Based Bag: " << endl;
}
else
{
    bagPtr = new LinkedBag<string>();
    cout << "Testing the Link-Based Bag: " << endl;
} // end if
```

```
cout << "The initial bag is empty." << endl;
bagTester(bagPtr);
delete bagPtr;
bagPtr = nullptr;
```

To accommodate the data type of bagPtr, we need to change the parameter lists of the functions in our test program as follows:

```
void displayBag(BagInterface<string>* bagPtr)
```

and

```
void bagTester(BagInterface<string>* bagPtr)
```

Finally, we must change the notation used to call methods on the instances of bagPtr, since it is a pointer. For example,

```
bag.isEmpty()
must be changed to
bagPtr->isEmpty()
```

Listing 4-4 is a complete listing of the modified test program for core methods of classes that are implementations of the ADT bag.

```
LISTING 4-4 A program that tests the core methods of classes that are derived from the abstract class BagInterface
#include "BagInterface.h"
#include "ArrayBag.h"
#include "LinkedBag.h"
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

void displayBag(BagInterface<string>* bagPtr)
{
   cout << "The bag contains " << bagPtr->getCurrentSize()
        << " items:" << endl;
   vector<string> bagItems = bagPtr->toVector();
   bagPtr->toVector(bagItems);
   int numberOfEntries = bagItems.size();
   for (int i = 0; i < numberOfEntries; i++)
   {
      cout << bagItems[i] << " ";
   }  // end for
   cout << endl << endl;
}  // end displayBag

void bagTester(BagInterface<string>* bagPtr)
{
   cout << "isEmpty: returns " << bagPtr->isEmpty()
        << "; should be 1 (true)" << endl;
   string items[] = {"one", "two", "three", "four", "five", "one"};
   cout << "Add 6 items to the bag: " << endl;
   for (int i = 0; i < 6; i++)
   {
      bagPtr->add(items[i]);
   }  // end for

   displayBag(bagPtr);

   cout << "isEmpty: returns " << bagPtr->isEmpty()
        << "; should be 0 (false)" << endl;
   cout << "getCurrentSize: returns " << bagPtr->getCurrentSize()
        << "; should be 6" << endl;
   cout << "Try to add another entry: add(\"extra\") returns "
        << bagPtr->add("extra") << endl;
}  // end bagTester

int main()
{
   BagInterface<string>* bagPtr = nullptr;
   char userChoice;
   cout << "Enter 'A' to test the array-based implementation\n";
   cout << " or 'L' to test the link-based implementation: ";
   cin >> userChoice;
   if (toupper(userChoice) == 'A')
   {
       bagPtr = new ArrayBag<string>();
       cout << "Testing the Array-Based Bag: " << endl;
   }
   else
   {
       bagPtr = new LinkedBag<string>();
       cout << "Testing the Link-Based Bag: " << endl;
   } // end if
   cout << "The initial bag is empty. " << endl;
   bagTester(bagPtr);
   delete bagPtr;
   bagPtr = nullptr;
   cout << "All done!" << endl;
   return 0;
} // end main
```

Sample Output 1
```
Enter 'A' to test the array-based implementation
or 'L' to test the link-based implementation: A
Testing the Array-Based Bag:
The initial bag is empty.
isEmpty: returns 1; should be 1 (true)
Add 6 items to the bag:
The bag contains 6 items:
one two three four five one
isEmpty: returns 0; should be 0 (false)
getCurrentSize: returns 6; should be 6
Try to add another entry: add("extra") returns 0
All done!
```

Sample Output 2
```
Enter 'A' to test the array-based implementation
or 'L' to test the link-based implementation: L
Testing the Link-Based Bag:
The initial bag is empty.
isEmpty: returns 1; should be 1 (true)
Add 6 items to the bag:
The bag contains 6 items:
one five four three two one
isEmpty: returns 0; should be 0 (false)
getCurrentSize: returns 6; should be 6
Try to add another entry: add("extra") returns 1
All done!
```

### Question 15

Revise the program in Listing 4-4 so that it tests first the array-based implementation and then the link-based implementation. Ensure that the program does not have a memory leak.
