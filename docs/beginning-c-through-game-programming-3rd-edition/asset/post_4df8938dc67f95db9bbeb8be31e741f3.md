
note is that after the Greet() message is displayed, the function ends and toDestroy is ready to be destroyed. Fortunately, toDestroy’s destructor is automatically called just before this happens. The destructor displays Destructor called and deletes the string object equal to "Rover" that’s on the heap, cleaning up after itself and leaking no memory. The destructor doesn’t do anything with the m_Age data member. That’s perfectly fine since m_Age isn’t on the heap, but part of toDestroy and will be properly disposed of right along with the rest of the Critter object.

## Hint

When you have a class that allocates memory on the heap, you should write a destructor that cleans up and frees that memory.

## Declaring and Defining Copy Constructors

Sometimes an object is copied automatically for you. This occurs when an object is:

- Passed by value to a function
- Returned from a function
- Initialized to another object through an initializer
- Provided as a single argument to the object’s constructor

The copying is done by a special member function called the copy constructor. Like constructors and destructors, a default copy constructor is supplied for you if you don’t write one of your own. The default copy constructor simply copies the value of each data member to data members of the same name in the new object—a member-wise copy.

For simple classes, the default copy constructor is usually fine. However, when you have a class with a data member that points to a value on the heap, you should consider writing your own copy constructor. Why? Imagine a Critter object that has a data member that’s a pointer to a string object on the heap. With only a default copy constructor, the automatic copying of the object would result in a new object that points to the same single string on the heap because the pointer of the new object would simply get a copy of the address stored in
the pointer of the original object. This member-wise copying produces a shallow copy, in which the pointer data members of the copy point to the same chunks of memory as the pointer data members in the original object.

Let me give you a specific example. If I hadn’t written my own copy constructor in the Heap Data Member program, when I passed a Critter object by value with the following function call, the program would have automatically made a shallow copy of crit called aCopy that existed in testCopyConstructor().

```
testCopyConstructor(crit);
```

aCopy’s m_pName data member would point to the exact same string object on the heap as crit’s m_pName data member does. Figure 9.8 shows you what I mean. Note that the image is abstract since the name of the critter is actually stored as a string object, not a string literal.

![](img/34f09be0ed6217c465debc4490197d4f_332_0.png)

## Figure 9.8

If a shallow copy of crit were made, both aCopy and crit would have a data member that points to the same chunk of memory on the heap.

Why is this a problem? Once testCopyConstructor() ends, aCopy’s destructor is called, freeing the memory on the heap pointed to by aCopy’s m_pName data member. Because of this, crit’s m_pName data member would point to memory that has been freed, which would mean that crit’s m_pName data member would be a dangling pointer! Figure 9.9 provides you with a visual representation of this. Note that the image is abstract since the name of the critter is actually stored as a string object, not a string literal.

What you really need is a copy constructor that produces a new object with its own chunk of memory on the heap for each data member that points to a heap object—a deep copy. That’s what I do when I define a copy constructor for the

![](img/34f09be0ed6217c465debc4490197d4f_333_0.png)

## Figure 9.9

If the shallow copy of the Critter object were destroyed, the memory on the heap that it shared with the original object would be freed. As a result, the original object would have a dangling pointer.

class, which replaces the default one provided by the compiler. First, inside the class definition, I declare the copy constructor:

```
Critter(const Critter& c);    //copy constructor prototype
```

Next, outside the class definition, I define the copy constructor:

```
Critter::Critter(const Critter& c)    //copy constructor definition
{
    cout << "Copy Constructor called\n";
    m_pName = new string(*(c.m_pName));
    m_Age = c.m_Age;
}
```

Just like this one, a copy constructor must have the same name as the class. It returns no value, but accepts a reference to an object of the class—the object that needs to be copied. The reference should be made a constant reference to protect the original object from being changed during the copy process.

The job of a copy constructor is to copy any data members from the original object to the copy object. If a data member of the original object is a pointer to a value on the heap, the copy constructor should request memory from the heap, copy the original heap value to this new chunk of memory, and then point the appropriate copy object data member to this new memory.

When I call testCopyConstructor() by passing crit to the function by value, the copy constructor I wrote is automatically called. You can tell this because the text Copy Constructor called. appears on the screen. My copy constructor creates a new Critter object (the copy) and accepts a reference to the original in c.

With the line m_pName = new string(*(c.m_pName));, my copy constructor allocates a new chunk of memory on the heap, gets a copy of the string pointed to by the original object, copies it to the new memory, and points the m_pName data member of the copy to this memory. The next line, m_Age = c.m_Age; simply copies the value of the original’s m_Age to the copy’s m_Age data member. As a result, a deep copy of crit is made, and that’s what gets used in testCopyConstructor() as aCopy.

You can see that the copy constructor worked when I called aCopy’s Greet() member function. In my sample run, the member function displayed a message, part of which was I’m Poochie and I’m 5 years old. This part of the message shows that aCopy correctly got a copy of the values of the data members from the object crit. The second part of the message, &m_pName: 73F2ED48003AF660, shows that the string object pointed to by the data member m_pName of aCopy is stored in a different chunk of memory than the string pointed to by the data member m_pName of crit, which is stored at memory location 73F2ED48003AF78C, proving that a deep copy was made. Remember that the memory addresses displayed in my sample run may be different from the ones displayed when the program is run again. However, the key here is that the addresses stored in crit’s m_pName and aCopy’s m_pName are different from each other.

When testCopyConstructor() ends, the copy of the Critter object used in the function, stored in the variable aCopy, is destroyed. The destructor frees the chunk of memory on the heap associated with the copy, leaving the original Critter object, crit, created in main(), unaffected. Figure 9.10 shows the results. Note that the image is abstract since the name of the critter is actually stored as a string object, not a string literal.

![](img/34f09be0ed6217c465debc4490197d4f_334_0.png)

Figure 9.10
With a proper copy constructor, the original and the copy each point to their own chunk of memory on the heap. Then, when the copy is destroyed, the original is unaffected.

## Hint

> When you have a class with data members that point to memory on the heap, you should consider writing a copy constructor that allocates memory for a new object and creates a deep copy.

## Overloading the Assignment Operator

When both sides of an assignment statement are objects of the same class, the class’ assignment operator member function is called. Like a default copy constructor, a default assignment operator member function is supplied for you if you don’t write one of your own. Also like the default copy constructor, the default assignment operator provides only member-wise duplication.

For simple classes, the default assignment operator is usually fine. However, when you have a class with a data member that points to a value on the heap, you should consider writing an overloaded assignment operator of your own. If you don’t, you’ll end up with shallow copies of objects when you assign one object to another. To avoid this problem, I overloaded the assignment operator for Critter. First, inside the class definition, I write the declaration:

```
Critter& Critter::operator=(const Critter& c);  //overloaded assignment op
```

Next, outside the class definition, I write the member function definition:

```
Critter& Critter::operator=(const Critter& c)  //overloaded assignment op def
{
    cout << "Overloaded Assignment Operator called\n";
    if (this != &c)
    {
        delete m_pName;
        m_pName = new string(*(c.m_pName));
        m_Age = c.m_Age;
    }
    return *this;
}
```

Notice that the member function returns a reference to a Critter object. For robust assignment operation, return a reference from the overloaded assignment operator member function.
