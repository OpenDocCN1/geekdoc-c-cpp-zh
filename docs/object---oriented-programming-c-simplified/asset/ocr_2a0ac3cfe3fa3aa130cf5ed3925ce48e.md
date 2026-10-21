# 4.6 MALLOC VS NEW

There are numbers of differences between the two:

+   1. **malloc** cannot be overloaded whereas **new** can be.
+   2. The new operator can be used to create objects.
+   3. The default return type for malloc is **void *** whereas new returns the appropriate pointer type *i.e.*, int in case of int, float in case of float and pointer to user defined data types when memory is allocated for objects or structures.
+   4. **new** operator automatically calculates size of object depending upon data type. No need to use **sizeof** operator.

# 4.7 POINTER MEMBER OPERATORS

There are three operators which are used with pointers to members or pointer to objects. It is advised that you first clear your concepts of class then refer this section. The three operations are :

+   1. :: * known as pointer to member decelerator.
+   2. ->* known as pointer to member dereference operator (through pointer).
+   3. .* known as pointer to member dereference operator (through value).

To create a pointer to a member of class :: * operator is used. The general syntax is:

```
data_type class_name :: *ptr_name =&class_name :: member _name;
```

For example, for a class demo having an int data member named data, pointer can be declared as :

```
int demo :: * ptr = &demo :: data;
```

To understand it more clearly recall how to create a pointer to an integer and store address of data. We will be written as:

```
int * ptr = &data;
```

Now on the left side of = operator between int and *ptr simply insert demo :: and on the right side of = operator between & and data insert demo :: . What you get ?

```
int demo :: * ptr = &demo :: data;
```

See how it is easy to define pointer to a class member.

After defining pointer ptr it can be used as:

```
demo d;

d.*ptr = 20; // assign value 20 to num of object d.
cout<<d.num<<endl; //display value 20.
```

Once a pointer has been created as shown in the above manner it will be available for all the objects created for the class. Similar to creating pointer for the data member of the class we can also create pointers for the objects also. For a class demo :

```
demo d;
demo *ptr = &d;
```