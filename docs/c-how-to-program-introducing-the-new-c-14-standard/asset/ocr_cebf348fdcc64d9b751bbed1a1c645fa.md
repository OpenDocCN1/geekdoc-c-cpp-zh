# 3.4 *Account* Class: Initializing
Objects with Constructors

As mentioned in **Section 3.3**, when an `Account` object is created, its `string` data member `name` is initialized to the empty `string` by *default*—we’ll discuss how that occurs shortly. But what if you want to provide a name when you first *create* an `Account` object? Each class can define a **constructor** that specifies *custom initialization* for objects of that class. A constructor is a special member function that *must* have the *same name* as the class. C++ *requires* a constructor call when *each* object is created, so this is the ideal point to initialize an object’s data members.^8

8. In Section 9.6, you’ll learn that classes can have multiple constructors.

Like member functions, a constructor can have parameters—the corresponding argument values help initialize the object’s data members. For example, you can specify an `Account` object’s name when the object is created, as you’ll do in line 11 of **Fig. 3.5**:

```
```cpp
Account account1{"Jane Green"};
```
```