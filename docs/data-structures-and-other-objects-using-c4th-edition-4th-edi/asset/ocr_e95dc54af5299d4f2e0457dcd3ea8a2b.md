+   - The function has only one parameter, addend. This is the right-hand bag in an expression such as `first_bag += second_bag`. The left-hand bag is the bag that activates `+=` and that has its contents altered.

+   - We use the name addend for the parameter, meaning “something to be added,” but you may use whatever name you like.

**The bag's CAPACITY.** That's the end of our list of functions, and we're almost ready to write the header file. But first, we describe one more handy C++ feature that is related to how we will store the items in a bag.

Our plan is for bounded bags that can hold 30 items each. (Later we will remove this restriction, providing an unbounded bag class.) There is nothing magic about the number 30—we just picked it as a conveniently small size for our first bags. Later, we might want to change the size to 30, allowing bags that hold 42 or 5000 or some other number of items. To make it easy to change the bag's size, and also to make our programs more readable, we will use a name such as CAPACITY rather than simply using the number 30.

The best way to define CAPACITY is as a static member constant, as shown in the example here:

```
```cpp
class bag
{
public:
    typedef int value_type;
    typedef std::size_t size_type;
    static const size_type CAPACITY = 30;
    ...
```
```

The keyword const has the same meaning that we have seen with other constant declarations, so that the value of CAPACITY is defined once and cannot be changed while the program is running.

The keyword static modifies the definition in a useful way. Usually each object has its own copy of each member variable. But when the keyword static is used with a class member, it means that all of the class's objects use the same value. This is different. For example, with the bag's static member constant, every bag has the same CAPACITY of 30. In fact, the only reason that we can set the CAPACITY to 30 within the class definition is because every bag has the same value for CAPACITY. When a program declares a bag b, the program can refer to the capacity with the usual notation for selecting a member: b.CAPACITY. Because every bag has the same capacity, a program can also refer to a bag's capacity using the bag :: “scope resolution operator,” as shown in this example:

```
```cpp
bag b;
cout << "The capacity of b is " << b.CAPACITY << endl;
cout << "Every bag has capacity " << bag::CAPACITY << endl;
```
```

As shown in this example, we recommend all uppercase letters for the name of any constant. This makes it easy to recognize which values are constant.