As an example, here is a sequence of function calls for a bag called first_bag:

```
bag first_bag;
first_bag.insert(8);
first_bag.insert(4);
first_bag.insert(8);
```

After these statements, first_bag contains two 8s and a 4.

After these statements are executed, first_bag contains three integers: the number 4 and two copies of the number 8. It is important to realize that a bag can contain many copies of the same integer, such as this example with two copies of 8.

Notice that the entry parameter is a const reference parameter. This may seem strange since the usual purpose of a const reference parameter is to improve efficiency when a parameter is a large object. Integers are not large, but we may later change the value_type to something that is large. With this in mind, we will use const reference parameters for value_type parameters, whenever this is possible (i.e., whenever the function's implementation does not change the value of the parameter).

# The count member function.

This is a constant member function that determines how many copies of a particular number are in a bag. The prototype uses size_type:

```
size_type count(const value_type& target) const;
```

The activation of count(n) returns the number of occurrences of n in a bag. For example, if first_bag contains the number 4 and two copies of the number 8, then we will have these values:

```
cout << first_bag.count(1) << endl; <-- Prints 0
cout << first_bag.count(4) << endl; <-- Prints 1
cout << first_bag.count(8) << endl; <-- Prints 2
```

# The erase_one and erase member functions.

These two member functions have the following prototypes:

```
bool erase_one(const value_type& target);
size_type erase(const value_type& target);
```

Provided that the target is actually in the bag, the erase_one function removes one copy of target and returns true. If target is not in the bag, attempting to erase one copy has no effect on the bag, and the function returns false. The erase function removes all copies of the target; its return value tells how many copies were removed (which could be zero).

![](bbox=[0.75, 0.16, 0.88, 0.32])