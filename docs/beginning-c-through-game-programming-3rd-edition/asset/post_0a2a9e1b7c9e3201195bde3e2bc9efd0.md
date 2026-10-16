
If I were to call this function, memory would be lost forever. (Okay, it would be lost until the program ended.) The problem is that `drip1`, which is the only connection to the newly acquired chunk of memory on the heap, is a local variable and ceases to exist when the function `leak1()` ends. So, there’s no way to free the allocated memory. Take a look at Figure 9.4 for a visual representation of how the leak occurs.

![](img/34f09be0ed6217c465debc4490197d4f_324_0.png)

**Figure 9.4** The memory that stores 30 can no longer be accessed to be freed, so it has leaked out of the system.

To avoid this memory leak, I could do one of two things. I could use `delete` to free the memory in `leak1()`, or I could return a copy of the pointer `drip1`. If I choose the second option, I have to make sure to free this memory in some other part of the program.

The second function that creates a memory leak is `leak2()`.

```
void leak2()
{
    int* drip2 = new int(50);
    drip2 = new int(100);
    delete drip2;
}
```

This memory leak is a little more subtle, but there is still a leak. The first line in the function body, `int* drip2 = new int(50);`, allocates a new piece of memory on the heap, assigns 50 to it, and has `drip2` point to that piece of memory. So far, so good. The second line, `drip2 = new int(100);`, points `drip2` to a new piece of memory on the heap, which stores the 100. The problem is that the memory on the heap that stores 50 now has nothing pointing to it, so there is no way for the program to free that memory. As a result, that piece of memory has essentially leaked out of the system. Check out Figure 9.5 for a visual representation of how the leak occurs.

![](img/34f09be0ed6217c465debc4490197d4f_325_0.png)

**Figure 9.5** By changing `drip2` so that it points to the memory that stores 100, the memory that stores 50 is no longer accessible and has leaked out of the system.

The last statement of the function, `delete drip2;`, frees the memory that stores 100, so this won’t be the source of another memory leak. But remember, the memory on the heap that stores 50 has still leaked out of the system. Also, I don’t worry about `drip2`, which technically has become a dangling pointer, because it will cease to exist when the function ends.

## Working with Data Members and the Heap

You’ve seen how you can use aggregation to declare data members that store objects, but you can also declare data members that are pointers to values on the heap. You might use a data member that points to a value on the heap for some of the same reasons you would use pointers in other situations. For example, you might want to declare a data member for a large 3D scene; however, you might only have access to the 3D scene through a pointer. Unfortunately, problems can arise when you use a data member that points to a value on the heap because of the way that some default object behaviors work. But you can avoid these issues by writing member functions to change these default behaviors.

### Introducing the Heap Data Member Program

The Heap Data Member program defines a new type of critter with a data member that is a pointer, which points to an object stored on the heap. The class defines a few new member functions to handle situations in which an object is destroyed, copied, or assigned to another object. The program destroys, copies, and assigns objects to show that the objects behave as you’d expect, even with data members pointing to values on the heap. Figure 9.6 shows the results of the Heap Data Member program.

![](img/34f09be0ed6217c465debc4490197d4f_326_0.png)

**Figure 9.6** Objects, each with a data member that points to a value on the heap, are instantiated, destroyed, and copied.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 9 folder; the filename is `heap_data_member.cpp`.

```
//Heap Data Member
//Demonstrates an object with a dynamically allocated data member

#include <iostream>
#include <string>

using namespace std;

class Critter
{
public:
    Critter(const string& name = "", int age = 0);
    ~Critter();                        //destructor prototype
    Critter(const Critter& c);         //copy constructor prototype
    Critter& operator=(const Critter& c);  //overloaded assignment op
    void Greet() const;

private:
    string* m_pName;
    int m_Age;
};

Critter::Critter(const string& name, int age)
{
    cout << "Constructor called\n";
    m_pName = new string(name);
    m_Age = age;
}

Critter::~Critter()                     // destructor definition
{
    cout << "Destructor called\n";
    delete m_pName;
}

Critter::Critter(const Critter& c)      // copy constructor definition
{
    cout << "Copy Constructor called\n";
    m_pName = new string(*(c.m_pName));
    m_Age = c.m_Age;
}

Critter& Critter::operator=(const Critter& c)  // overloaded assignment op definition
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

void Critter::Greet() const
{
    cout << "I'm " << *m_pName << " and I'm " << m_Age << " years old.\n";
    cout << "&m_pName: " << &m_pName << endl;
}

void testDestructor();
void testCopyConstructor(Critter aCopy);
void testAssignmentOp();

int main()
{
    testDestructor();
    cout << endl;

    Critter crit("Poochie", 5);
    crit.Greet();
    testCopyConstructor(crit);
    crit.Greet();
    cout << endl;

    testAssignmentOp();

    return 0;
}

void testDestructor()
{
    Critter toDestroy("Rover", 3);
    toDestroy.Greet();
}

void testCopyConstructor(Critter aCopy)
{
    aCopy.Greet();
}

void testAssignmentOp()
{
    Critter crit1("crit1", 7);
    Critter crit2("crit2", 9);
    crit1 = crit2;

    crit1.Greet();
    crit2.Greet();
    cout << endl;

    Critter crit3("crit", 11);
    crit3 = crit3;
    crit3.Greet();
}
```

### Declaring Data Members that Point to Values on the Heap

To declare a data member that points to a value on the heap, you first need to declare a data member that’s a pointer. That’s just what I do in Critter with the following line, which declares `m_pName` as a pointer to a string object.

```
string* m_pName;
```

In the class constructor, you can allocate memory on the heap, assign a value to the memory, and then point a pointer data member to the memory. That’s what I do in the constructor definition with the following line, which allocates memory for a string object, assigns `name` to it, and points `m_pName` to that chunk of memory on the heap.

```
m_pName = new string(name);
```

I also declare a data member that is not a pointer:

```
int m_Age;
```

This data member gets its value in the constructor the way you’ve seen before, with a simple assignment statement:

```
m_Age = age;
```

You’ll see how each of these data members is treated differently as Critter objects are destroyed, copied, and assigned to each other.

Now, the first object with a data member on the heap is created when `main()` calls `testDestructor()`. The object, `toDestroy`, has an `m_pName` data member that points to a string object equal to `"Rover"` that’s stored on the heap. Figure 9.7 provides a visual representation of the Critter object. Note that the image is abstract because the name of the critter is actually stored as a string object, not a string literal.

![](img/34f09be0ed6217c465debc4490197d4f_330_0.png)

**Figure 9.7** A representation of a Critter object. The string object equal to `"Rover"` is stored on the heap.

### Declaring and Defining Destructors

One problem that can occur when a data member of an object points to a value on the heap is a memory leak. That’s because when the object is deleted, the pointer to the heap value disappears along with it. If the heap value remains, it produces a memory leak. To avoid a memory leak, the object should clean up after itself before it is destroyed by deleting its associated heap value. Fortunately, there’s a member function, the destructor, that’s called just before an object is destroyed, which can be used to perform the necessary cleanup.

A default destructor, which is created for you by the compiler if you don’t write your own, doesn’t attempt to free any memory on the heap that a data member might point to. This behavior is usually fine for simple classes, but when you have a class with data members that point to values on the heap, you should write your own destructor so you can free the memory on the heap associated with an object before the object disappears, avoiding a memory leak. That’s what I do in the Critter class. First, inside the class definition, I declare the destructor. Notice that a destructor has the name of the class preceded by `~` (the tilde character) and does not have any parameters or return a value.

```
Critter::~Critter()                 //destructor definition
{
    cout << "Destructor called\n";
    delete m_pName;
}
```

In `main()`, I put the destructor to the test when I call `testDestructor()`. The function creates a Critter object, `toDestroy`, and invokes its `Greet()` method, which displays `I’m Rover and I’m 3 years old. &m_pName: 73F2ED48003AF644`. The message provides a way to see the values of the object’s `m_Age` data member and the string pointed to by its `m_pName` data member. But it also displays the address of the string on the heap stored in the pointer `m_pName`. The important thing to
