
# EXERCISES 12.2

+   1. (Practice) Enter and run Programs 12.2 and 12.3 so that you understand the relationship between function calls in each program.

+   2. (Review) Describe the difference between static binding and dynamic binding.

+   3. (Review) Describe the difference between a virtual function and a nonvirtual function.

+   4. (Review) Explain what polymorphism is and give an example of polymorphic behavior.

+   5. (Review) Describe the two methods C++ provides for implementing polymorphism.

+   6. (Review) Explain whether the multiplication operator provided for integer and double-precision built-in types is an example of overloading or polymorphism.

## 12.3 Dynamic Object Creation and Deletion

As each object is defined in a program, the compiler designates enough storage for it; this storage is subsequently assigned from a pool of computer memory locations before the program runs. After memory locations have been assigned, they remain fixed for the object's lifetime or until the program finishes running. For example, if a main() function declares three Date objects, the storage for these objects remains fixed from the point of their definition until main() completes execution.

An alternative to this fixed allocation of memory storage locations is dynamic allocation of memory, in which the amount of storage to be allocated is assigned, as requested, at runtime instead of being fixed at compile time. Dynamic allocation of memory is useful when dealing with lists and objects because it allows expanding the list as new items are added and contracting the list as items are deleted. For object-oriented programs, it allows creating and destroying new objects as required.

As an example of dynamic object creation, say you're creating a program designed to track the flow of customers at a large outlet chain's self-checkout registers. You don't know in advance the number of transactions taking place at each register. However, by using dynamic allocation, the program can create an object as each checkout transaction occurs for tracking customer use of the checkout process. This object might consist of the number of items checked out and the arrival time of each customer at the register. Although the class's do-nothing methods are completed later, the following class adequately defines the information this object needs. In reviewing this class, notice the shaded constructor and destructor methods:

```
// class declaration section
class Checkout
{
private:
    int numItems;
    double arrivalTime;
```

```
```cpp
public:
    Checkout();    // constructor
    // the following is an inline destructor
    ~Checkout()
        { cout << "!!! This Customer object has been deleted !!!!\n"; }
    void showObject();
    void getItems(){return;}   // inline do-nothing methods
    void getTime(){return;}    // will be used in Program 12.5
};

// class implementation section
Checkout::Checkout() // constructor
{
    cout << "\n**** A new Customer object has been created ****\n";
    numItems = 5;
    arrivalTime = 2.5;
}

void Checkout::showObject()
{
    cout << "     For this object:\n";
    cout << "     numItems = " << numItems
         << "     arrivalTime = " << arrivalTime << endl;
    return;
}
```
```

The constructor method causes the following display whenever an object is created:

**** A new Customer object has been created ****

Similarly, the destructor method, which is called automatically when an object is destroyed, causes the following message to be displayed:

!!! This Customer object has been deleted !!!!

These messages are included to help you monitor creation and deletion of an object by using dynamic allocation. Table 12.2 describes two C++ operators, new and delete, that provide this capability. (These operators require the new header file.)

**Table 12.2  Dynamic Allocation and Deallocation Operators**

| Operator Name | Description |
|---|---|
| `new` | Reserves the correct number of bytes for the variable or object type requested by the declaration. Returns the address of the first reserved location or a NULL value if not enough memory is available. |
| `delete` | Releases previously reserved memory. The address of the first reserved location must be passed as an argument to the operator. |

After an object has been dynamically created, it can be accessed only by using the address the new operator returns. So like the `this` pointer, the newly created object’s address must be stored in a pointer variable. The mechanism for doing this is rather simple. For example, the statement

```
Checkout *anotherTrans = new Checkout;
```

declares anotherTrans as a pointer to a Checkout object, reserves memory for the object, and places this newly created object’s address in the anotherTrans pointer.

This dynamic creation of a Checkout object can also be made in two steps. The first step is to declare a pointer variable with a declaration statement. Then, when an object is actually required, a request can be made to create the object. When the object is created, its address is assigned to the previously declared pointer. Following are the two required statements:

```
Checkout *anotherTrans;    // declares anotherTrans as a pointer
                           // that can store the address
                           // of a Checkout object

anotherTrans = new Checkout;    // creates a new Checkout object and
                                // stores this object's address in
                                // the pointer named anotherTrans
```

The expression `new Checkout` on the right of the equals sign creates a new Checkout object. The address returned by the new operator is then assigned to the pointer variable on the left of the equals sign. These two statements are the first two shaded statements in Program 12.4’s `main()` function.

# Program 12.4

```
#include <iostream>
using namespace std;

// class declaration section
class Checkout
{
    private:
        int numItems;
        double arrivalTime;

    public:
        Checkout();    // the constructor
        // the following is an inline destructor
        ~Checkout()
        {cout << "!!!! This Customer object has been deleted !!!!\n";}

void showObject();
void getItems(){return;};  // inline do-nothing methods
void getTime(){return;};  // will be used in Program 12.5
};

// class implementation section
Checkout::Checkout()  // constructor
{
    cout << "\n**** A new Customer object has been created ****\n";
    numItems = 5;
    arrivalTime = 2.5;
}

void Checkout::showObject()
{
    cout << "  For this object:\n";
    cout << "      numItems = " << numItems
         << "      arrivalTime = " << arrivalTime << endl;
    return;
}

int main()
{
    Checkout *anotherTrans;  // pointer to a Checkout object
    int i, howMany;

    cout << "Enter the number of transactions to be created: ";
    cin >> howMany;

    for(i = 1; i <= howMany; i++)
    {
        anotherTrans = new Checkout;  // create a new Checkout object

        // display the address of the created object
        cout << "The memory address of this object is: " << anotherTrans << endl;
        anotherTrans->showObject();  // display contents of this object
        delete anotherTrans;  // delete the object
    }

    return 0;
}
```

Following is a sample output produced by Program 12.4:

```
Enter the number of transactions to be created: 1

**** A new Customer object has been created ****
The memory address of this object is: 003B65A0

For this object:
numItems = 5    arrivalTime = 2.5
!!!! This Customer object has been deleted !!!!
```

Take a look at how this output was produced. The first shaded statement in main()—Checkout *anotherTrans;—defines a pointer to a Checkout object. The user is then prompted to enter the number of dynamic objects to be created, which in this case is one.

The next shaded statement—anotherTrans = new Checkout;—creates a new Checkout object and stores its address in the anotherTrans variable. This stored address is then displayed by inserting the pointer's name in a cout stream (the third shaded statement). Because the content of a pointer variable is a value, this value, even though it happens to be an address, can be displayed in this manner. Figure 12.6 shows the allocation of memory corresponding to this address.

![](img/e9bf940282dfb289356f077151cc69dd_575_0.png)

# Figure 12.6 The memory allocation produced by a sample run of Program 12.4

Now notice the fourth shaded statement, which shows the notation used to apply a member method to a newly created object. The statement anotherTrans->showObject(); applies the showObject() method to the object whose address resides in the pointer variable anotherTrans. Because dynamically created objects don't have symbolic names, they can be accessed only by using the address information in the pointer variable. However, as explained in Section 11.2, the notation anotherTrans->showObject(); can be replaced by (*anotherTrans).showObject();.

Finally, the last shaded statement in the main() function deletes the object and returns the memory previously assigned to it to the computer's operating system.² Deleting dynamically created objects when their usefulness ends is crucial. Otherwise, as new objects are created, the computer starts to "eat up" available memory space, especially if the same pointer is used in creating a new object before the old object is deleted. The reason is that after an existing object's address is overwritten with a new object's address, there's no way for the system to reclaim the memory. This condition is referred to as memory leak. In the worst case,

> ²The allocated storage is returned automatically to the heap (a computer's free storage area) when the program has finished running. It is, however, a good practice to restore allocated storage back to the heap by using delete when the memory is no longer needed, especially for large programs that make numerous requests for additional storage areas.
