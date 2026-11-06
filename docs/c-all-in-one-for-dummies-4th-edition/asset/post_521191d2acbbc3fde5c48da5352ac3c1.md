
## LISTING 3-2: Customizing the Copying of Instances

```cpp
#include <iostream>

using namespace std;

class Copyable {
protected:
    static int NextAvailableID;
    int UniqueID;
public:
    int SomeNumber;
    int GetID() { return UniqueID; }
    Copyable();
    Copyable(int x);
    Copyable(const Copyable& source);
};

Copyable::Copyable() {
    UniqueID = NextAvailableID;
    NextAvailableID++;
}

Copyable::Copyable(int x) {
    UniqueID = NextAvailableID;
    NextAvailableID++;
    SomeNumber = x;
}

Copyable::Copyable(const Copyable& source) {
    UniqueID = NextAvailableID;
    NextAvailableID++;
    SomeNumber = source.SomeNumber;
}

int Copyable::NextAvailableID;

int main() {
    Copyable take1 = 100;
    Copyable take2;
    take2.SomeNumber = 200;
    Copyable take3 = take1;
    cout << take1.GetID() << " "
         << take1.SomeNumber << endl;
    cout << take2.GetID() << " "
         << take2.SomeNumber << endl;
    cout << take3.GetID() << " "
         << take3.SomeNumber << endl;
    return 0;
}
```

You see the following output when you run this application:

```text
0 100
1 200
2 100
```

You need to know two things about this code:

- **Copy constructor with const instance.** C++ has a rule where you must have a const instance to create a copy. If you leave off const, this line would not compile properly.
- **Copying the properties manually from one instance to the other.** Now that the class has its own copy constructor, the computer will not copy the members as it would when the code lacks a copy constructor.

Listing 3-2 uses a static member to keep track of what the next available UniqueID is. Remember that a class shares a single static member among all instances of the class. Therefore, you have only one instance of NextAvailableID, and it's shared by all the instances of class Copyable.

## When constructors go bad

Suppose that you're writing a class that will connect to the Internet and automatically download the latest weather report for the country of Upper Zamboni. The question is this: Do you put the code to connect to the Internet in the constructor or not?

People are often faced with this common design issue. Putting the initialization code in the constructor provides many advantages. For one, you can produce a usable instance without having to first create it and then call a separate method that does the initialization. In general, this approach works fine.

However, sometimes the initialization process can produce an error. For example, suppose that the constructor is unable to connect to the Internet. Remember: A constructor doesn't return a value. So you can't have it return, for example, a bool that would state whether it successfully did its work.

```cpp
class Container {
public:
  LittleInst first;
  LittleInst *second;
  Container();
};

Container::Container() {
  first.MyNumber = 1;
  second = new LittleInst;
  second->MyNumber = 2;
}
```

You see two classes, LittleInst and Container. The Container class holds an instance of LittleInst (the property called first) and a pointer to LittleInst. The constructor sets up the two LittleInst instances. For first, it already exists, and all you have to do is configure first’s MyNumber member. But second is just a pointer, so the code creates the instance before it can configure the second MyNumber member. Thus we have two instances, one a pointer and one a regular instance.

Now suppose you use these classes like so:

```cpp
Container *inst = new Container;
delete inst;
```

Container has no destructor, so the concern is whether first and second get destroyed. Here’s the output you see:

```text
1
```

That’s the output from the LittleInst destructor. The number 1 goes with the first member. So you can see that first was destroyed, but second wasn’t.

![](img/128ab511de4e7360e167e3b15cdd5dd0_578_0.png)

Here’s the rule: When you delete an instance of a class, the members that are direct (that is, not pointers) are deleted as well. If you have any pointers, however, you must manually delete them in your destructor (or elsewhere).

Sometimes you may want an object to hold an instance of another class but want to keep the instance around after you delete the containing object. In that case, you wouldn’t delete the other instance in the destructor.

## Constructors, Destructors, and Exceptions

Here’s a modification to the `Container` class (found in the `Destructor02` example) that deletes the second instance:

```cpp
class Container {
public:
  LittleInst first;
  LittleInst *second;
  Container();
  ~Container() { delete second; }
};
```

Then, when you run these two lines again:

```cpp
Container *inst = new Container;
delete inst;
```

you see this output, which deletes both instances:

```text
2
1
```

In the preceding output, you can see that it deleted the second instance first. The reason is that the application calls the destructor before it destroys the direct members. In this case, when the code deleted the `Container` instance, the application first called the destructor before deleting the first member. That’s actually a good idea, because in the code for the destructor, you may want to do some work on the properties before they get wiped out.

### Virtually inheriting destructors

You can (and should) make destructors virtual — unlike constructors (the constructor can’t be virtual because when a constructor of a class is executed, there is no virtual table in the memory, which means no virtual pointer has been defined yet). The reason is that you can pass an instance of a derived class into a function that takes a base class, like this:

```cpp
void ProcessAndDelete(DeleteMe *inst) {
  cout << inst->Number << endl;
  delete inst;
}
```

This function takes an instance of class `DeleteMe`, does some work on it, and deletes it. Now, suppose you have a class derived from `DeleteMe` — say, class `Derived`. Because of the rules of inheritance, you’re allowed to pass the instance of Derived into this function. But by the rules of polymorphism (as described in the “Specializing with polymorphism” section of Book 2, Chapter 3), if you want the ProcessAndDelete() function to call an overloaded method of Derived, you need to make the method virtual. That's the case with all destructors as well. The Destructor03 example, shown in Listing 3-3, demonstrates making destructors virtual.

### LISTING 3-3: Making the Destructors Virtual

```cpp
#include <iostream>

using namespace std;

class DeleteMe {
public:
  int Number;
  virtual ~DeleteMe();
};

class Derived : public DeleteMe {
public:
  virtual ~Derived();
};

DeleteMe::~DeleteMe() {
  cout << "DeleteMe::~DeleteMe()" << endl;
}

Derived::~Derived() {
  cout << "Derived::~Derived()" << endl;
}

void ProcessAndDelete(DeleteMe *inst) {
  cout << inst->Number << endl;
  delete inst;
}

int main() {
  DeleteMe *MyObject = new(Derived);
  MyObject->Number = 10;
  ProcessAndDelete(MyObject);
  return 0;
}
```

When you run this application, delete calls the destructor for `Derived`, which in turn calls the base class destructor. You can see how all this works thanks to the cout calls in the destructors. Here's the output:

```text
10
Derived::~Derived()
DeleteMe::~DeleteMe()
```

The first line is the output from ProcessAndDelete(). The middle line is the output from the Derived() destructor, and the third line is the output from the DeleteMe() destructor. The code passes in a Derived instance, and the application calls the Derived destructor.

Now try this: Remove virtual from the DeleteMe destructor:

```cpp
class DeleteMe {
public:
    int Number;
    ~DeleteMe();
};
```

When you compile and run the application, the application calls the base class destructor. Because ProcessAndDelete() takes a DeleteMe instance, you see this output:

```text
10
DeleteMe::~DeleteMe()
```

### ORDERING YOUR CONSTRUCTORS AND DESTRUCTORS

When you have constructors and destructors in a base and derived class and you create an instance of the derived class, remember the ordering: The computer first creates the members for the base class, and then the computer calls the constructor for the base class. Next, the computer creates the members of the derived class, and then the computer calls the constructor for the derived class.

The order for destruction is opposite. When you destroy an instance of a base class, first the computer calls the destructor for the derived class and then deletes the members of the derived class. Next, the computer calls the destructor for the base class and then deletes the members of the base class.
