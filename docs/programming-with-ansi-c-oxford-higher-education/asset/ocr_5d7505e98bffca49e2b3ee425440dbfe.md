to note that the pointer ItemsInterested here does not have any memory to store data; it is sharing the memory location with ItemArray.

If the values in the constructor are changed, it would inadvertently change the values in the passed array, ItemArray. This is similar to passing an array pointer for manipulating it similar to passing an array pointer for sorting functions.

The second case is a separate array into which the passed array has been copied, so, it would not have changed values even if the original passed array is changed. The original array is also immune to changes made to the array items in the constructor function. Exhibit 5.1 shows why copying pointer members is not correct.

> ## Exhibit 5.1 Copying pointer members is not correct
> 
> When a constructor uses new to initialize with a dynamic number of values passed to it at run-time, it cannot copy a pointer value. It results in one memory location being shared by multiple objects. Therefore, the changes carried out in the values of one object will reflect as changes in other object values.
> 
> Using dynamic memory allocation and giving a new object its own memory helps to avoid this problem by having separate copies of values. Hence, such cases demand dynamic allocation. It is not possible to use static allocation here because the number of items a customer would be interested in is not known in advance.

Objects as members of some other class Program 5.6 also shows how an object of a class becomes a data member of some other class (Item object becoming member of customer class). It is important to note that this object is not a normal data member; it is different from normal data members. This difference will be discussed when we learn about inheritance and containership in Chapter 9. When an object is defined as a member of some other class, it is treated differently from other members when the objects of that class are initialized.

# Dynamic allocation applied

It should be noted how the customers are initialized using a parameterized constructor. Items such as CustNo and CustName are initialized in a normal way. ItemsInterested is actually a pointer and cannot be initialized in the same way. When the constructor is called, the pointer is passed to an array containing Item objects to the constructor.

```
Steve = customer(2, "Steve Waugh", "Australia", ItemArray, 5);
```

Here, ItemArray is the name of an array. As in C, it is a static pointer to the array and points to the first item of the array, that is, it contains the address of the first item. As it is static, it cannot be assigned some other value later as done in a normal pointer variable. It is possible to pass any array with any valid length here. This program uses a single array with different starting points and different lengths. It is also possible to pass totally different arrays. In the first example, the array name itself is passed with the total items as five. Array name, as we have discussed earlier, is a pointer to the first item. So, it starts with the first item. In the second example, it starts with ItemArray + 2. It should be remembered that this notation is common in C programming and is also used in C++. It is the same as ItemArray[2]. It adds two to an item pointer variable and makes it point to the address of the third item of an array.

# Correct way to copy

We need to store an entire array of items and we do not have any space in the data member for it. We must solve this problem by obtaining memory for storing those elements dynamically. It should be remembered that the data member in this program