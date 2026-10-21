

```cpp
Item ItemArray[] = {Item(3,"Sandwiches"), Item(4,"PaperBags"), Item(5,"Napkins"), Item(6,"Toys"), Item(10,"Biscuits"), Item(9,"Pen"), Item(1,"Pencil"), Item(2,"Eraser")};

Steve = customer(2, "Steve Waugh", "Australia", ItemArray, 5);
Steve.ShowDetails();
customer Flintoff(3, "Flintoff the Captain", "England", ItemArray + 2, 6);
Flintoff.ShowDetails();
}
```

## Output

```text
Customer number is 2
Customer name is Steve Waugh
Customer address is Australia
Steve Waugh is interested in the following items:
Item number is 3

Customer number is 3
Customer name is Flintoff the Captain
Customer address is England
Flintoff the Captain is interested in the following items:
Item number is 5
Item number is 2
Item name is Eraser
```

## How the Program Works

As usual, let us dissect the program and try to understand what it is trying to accomplish. We will look at each section one by one.

### Dynamic initialization

In this program, the customers have a new data member, that is, a pointer to ItemsInterested. This data member is just a pointer and not an array. When a new customer is defined, an array containing the items that the customer is interested in is passed. The item here is itself an object of the class Item for which the memory is dynamic. Looking at the length of the array passed, the constructor creates a dynamic array in the allocated space, which is then used to store the passed values. At the end, the constructor stores the address of that memory in the pointer variable, so it is now possible to access the customer object with the required set of ItemsInterested. Now, the customer object is initialized with the items that the customer is interested in. The reader might wonder about the need for dynamic initialization and why it will not work if the passed value is just assigned to the pointer. Figures 5.1 and 5.2 show the difference between the cases without and with dynamic initialization.

```text
customer object when defined
Other fields
ItemsInterested → → Items are stored
... in a temporary array

customer object when constructor gets over
Other fields
ItemsInterested → → This is a dangling pointer.
... The memory may be allocated for some other purpose.
```

*Fig. 5.1 Without dynamic initialization*

![](img/0da15892b2796544fb447dc5727e9ab4_222_0.png)

*Fig. 5.2 With dynamic initialization*

### Need for dynamic initialization

If the passed array is deleted, the first type of initialization would lead to a dangling pointer whereas in the second case it is not affected. Moreover, if the passed array changes its values in the first case, ItemsInterested would change because we just point to that location, that is, we are sharing the data (the array that is passed) with the calling function. In Program 5.6, if the dynamic allocation part is omitted, the program would look as follows:

```cpp
// Erroneous code
customer(int TempCustNo, string TempCustName, string TempCustAddress, Item *TempItemsInterested, int TempTotalItems)
{
    CustNo = TempCustNo;
    CustName = TempCustName;
    CustAddress = TempCustAddress;
    ItemsInterested = TempItemsInterested; // the erroneous line
    TotalItems = TempTotalItems;
}
```

```cpp
// The following is a call to the constructor defined above
Steve = customer(2, "Steve Waugh", "Australia", ItemArray, 5);
```

Now, ItemsInterested will point to ItemArray (the passed array). If the values of ItemArray are changed or deleted, the ItemsInterested pointer would fetch changed values or garbage because it is pointing to the same location to which ItemArray is pointing. It is important to note that the pointer ItemsInterested here does not have any memory to store data; it is sharing the memory location with ItemArray.

If the values in the constructor are changed, it would inadvertently change the values in the passed array, ItemArray. This is similar to passing an array pointer for manipulating it, similar to passing an array pointer to sorting functions.

The second case is a separate array into which the passed array has been copied, so it would not have changed values even if the original passed array is changed. The original array is also immune to changes made to the array items in the constructor function. Exhibit 5.1 shows why copying pointer members is not correct.

> ### Exhibit 5.1 Copying pointer members is not correct
>
> When a constructor uses new to initialize with a dynamic number of values passed to it at run-time, it cannot copy a pointer value. It results in one memory location being shared by multiple objects. Therefore, the changes carried out in the values of one object will reflect as changes in other object values.
>
> Using dynamic memory allocation and giving a new object its own memory helps to avoid this problem by having separate copies of values. Hence, such cases demand dynamic allocation. It is not possible to use static allocation here because the number of items a customer would be interested in is not known in advance.

### Objects as members of some other class

Program 5.6 also shows how an object of a class becomes a data member of some other class (Item object becoming member of customer class). It is important to note that this object is not a normal data member; it is different from normal data members. This difference will be discussed when we learn about inheritance and containership in Chapter 9. When an object is defined as a member of some other class, it is treated differently from other members when the objects of that class are initialized.

### Dynamic allocation applied

It should be noted how the customers are initialized using a parameterized constructor. Items such as CustNo and CustName are initialized in a normal way. ItemsInterested is actually a pointer and cannot be initialized in the same way. When the constructor is called, the pointer to an array containing Item objects is passed to the constructor.

```cpp
Steve = customer(2, "Steve Waugh", "Australia", ItemArray, 5);
```

Here, ItemArray is the name of an array. As in C, it is a static pointer to the array and points to the first item of the array, that is, it contains the address of the first item. As it is static, it cannot be assigned some other value later as done in a normal pointer variable. It is possible to pass any array with any valid length here. This program uses a single array with different starting points and different lengths. It is also possible to pass totally different arrays. In the first example, the array name itself is passed with the total items as five. Array name, as we have discussed earlier, is a pointer to the first item. So, it starts with the first item. In the second example, it starts with ItemArray + 2. It should be remembered that this notation is common in C programming and is also used in C++. It is the same as ItemArray[2]. It adds two to an item pointer variable and makes it point to the address of the third item of an array.

### Correct way to copy

We need to store an entire array of items and we do not have any space in the data member for it. We must solve this problem by obtaining memory for storing those elements dynamically. It should be remembered that the data member in this program is not an array, but is merely a pointer. The memory needs to be dynamically allocated. It is interesting to see how ItemsInterested is initialized dynamically in the following example. TempTotalItems is the length of an array. The memory for an array of that length is obtained using the following statement:

```cpp
ItemsInterested = new Item[TempTotalItems];
```

Here, the memory space needed is available. Now, the pointer in the constructor becomes useful. The address of this memory (the dynamically generated array) is stored in the pointer variable, ItemsInterested. new makes it possible to do both in a single statement.

Then, for all items passed in the array, the ItemsInterested array of the object is initialized as follows:

```cpp
for(int i=0; i<TempTotalItems; ++i)
{
    ItemsInterested[i] = TempItemsInterested[i];
}
```

It can be seen that this solves the problem of memory allocation in cases where a priori knowledge of the number of items of the ItemsInterested array is not available. It is dynamically allocated and the array is available at run-time, which is what was needed.

Though this problem is solved, it is not without cost. Using dynamic allocation will invite more responsibilities. Moreover, copy constructors and overloaded assignment operators as well as destructors are also needed now. The reason for this is given in Exhibit 5.2.

> ### Exhibit 5.2 Memory leaks
>
> Dynamic initialization has a specific problem. When the memory is assigned dynamically for initializing an object, it is essential to deallocate it as well, when the object goes out of scope.
>
> Unlike in the case of other variables, where C++ does the deallocation as soon as the variable goes out of scope, it is not done here until the program execution is over. This problem is known as memory leak.
>
> C++11 has two important improvements; one is the garbage collector, which takes care of memory leaks, and the second one is that it has better ways of managing temporary objects.

## 5.11 COPY CONSTRUCTORS

It is possible to pass all types of arguments to a constructor except the object itself. It is obvious why this restriction is provided in C++. If an object is allowed to be passed to the constructor of the same object, for creating a single object, the constructor needs to create one more such object for passing to it while creating that object, and it needs to pass one more such object for creating that object and so on, which is an infinite process. Therefore, C++ would flag an error when a native object is passed to the constructor.

However, it is possible to pass the reference of the native object to the constructor, which, in a technical sense, is a pointer to the same type of object. This type of constructor is known as a copy constructor and it has an important use in C++. Before we study the importance of the copy constructor, we must understand the difference between initialization and assignment.

> We can pass all types of arguments to a constructor except the object itself.

