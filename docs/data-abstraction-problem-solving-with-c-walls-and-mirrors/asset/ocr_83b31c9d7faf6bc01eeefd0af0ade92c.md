# An Array-Based Implementation of the ADT Bag

Array defines the bag's capacity—that is, its maximum size—we define a constant whose value is this size. To hide these data members from the clients of the class, we make them private. Thus, we define the following private data members within the header file for our class:

```
static const int DEFAULT_CAPACITY = 50;
Item items[DEFAULT_CAPACITY]; // Array of bag items
int itemCount; // Current count of bag items
int maxItems; // Max capacity of the bag
```

Figure 3-2 illustrates these data members, assuming a bag of integers.

**Figure 3-2** Array-based implementation of the ADT bag

Array indices
| 0 | 1 | 2 | 3 | ... | 5 | 10 | 18 | ? | ... | maxItems-1 |
|---|---|---|---|---|---|---|---|---|---||
| k | 12 | 19 | 100 | | 5 | 18 | ? | | | |
itemCount | items

> **Note:** Data members should be private\By making a class's data members private, you control how a client can access or change their values. Doing so also makes debugging a program's logic easier. If the client could manipulate this data because the bag was public, you would not know where to look for.

# 3.2.1 The Header File

Having chosen the data members, knowing the details of BagInterface, which we developed in Chapter 1, we can write the header file shown in Listing 3-1 for our class bags. We name the class ArrayBag and give it a default constructor, which is sufficient for this example. Notice the small value given to the constant DEFAULT_CAPACITY. It enables us to fill a bag completely. After Interlude 2, we will be able to add another constructor that enables the client to set the capacity of the bag during program execution. We include the field maxItems in anticipation of this enhancement.
Also notice that we declare a private method indexOf. This method returns the index of the element within the array that contains a given entry. As you will see, we can use indexOf to make the methods contains and remove more time. You most likely would not decide to add indexOf to the header file until you work on the implementation of the public methods.

```
LISTING 3-1 The header file for the class ArrayBag
/**
 * Header file for an array-based implementation of the ADT bag.
@file ArrayBag.h */

#ifndef _ARRAY_BAG
#define _ARRAY_BAG

#include "BagInterface.h"

(continues)
```