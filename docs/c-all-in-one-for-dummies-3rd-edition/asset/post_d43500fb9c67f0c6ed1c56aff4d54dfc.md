
## Book 1

### Chapter 8 Working with Classes

This is just a simple function with no return type. It takes an object pointer as a parameter. For example, after you eat a block of cheese, you can call:

```
OneMoreCheeseGone(MyBlock);
```

Now consider this: If you have an object on the heap, it has no name. You access it through a pointer variable that points to it. But what if the code is currently executing inside a member function of an object? How do you refer to the object itself?

C++ has a secret variable that exists inside every member function: this. It's a pointer variable. The this variable always points to the current object. So if code execution is occurring inside a member function and you want to call OneMoreCheeseGone(), passing in the current object (or block of cheese), you would pass this.

The CheeseClass example shown in Listing 8-8 demonstrates this. The listing has four main parts. First is the definition for the class called Cheese. The class contains a couple of member functions.

Next is the function OneMoreCheeseGone() along with a global variable that it modifies. This function subtracts one from the global variable and stores a string in a member variable, status, of the object passed to it.

Next come the actual member functions for class Cheese. (We put these functions after the OneMoreCheeseGone() function because they call it. If we used a function prototype as a forward reference for OneMoreCheeseGone(), the order wouldn't matter.)

Finally we have main(), which creates two new instances of Cheese. Then it sets the global variable to 2, which keeps track of the number of blocks left. Next, it calls the eat function for the asiago cheese and rot for the limburger cheese. And then it prints the results of everything that happened: It displays the Cheese count, and it displays the status variable of each object.

#### Listing 8-8: Passing an Object from Inside Its Member Functions by Using the *this* Variable

```cpp
#include <iostream>

using namespace std;

class Cheese
{
public:
    string status;
    void eat();
    void rot();
};

int CheeseCount;

void OneMoreCheeseGone(Cheese *Block)
{
    CheeseCount--;
    Block->status = "Gone";
}

void Cheese::eat()
{
    cout << "Eaten up! Yummy" << endl;
    OneMoreCheeseGone(this);
}

void Cheese::rot()
{
    cout << "Rotted away! Yuck" << endl;
    OneMoreCheeseGone(this);
}

int main()
{
    Cheese *asiago = new Cheese();
    Cheese *limburger = new Cheese();

    CheeseCount = 2;

    asiago->eat();
    limburger->rot();

    cout << endl;
    cout << "Cheese count: " << CheeseCount << endl;
    cout << "asiago: " << asiago->status << endl;
    cout << "limburger: " << limburger->status << endl;

    return 0;
}
```

When you run the application in Listing 8-8, you see this output:

```text
Eaten up! Yummy
Rotted away! Yuck

Cheese count: 0
asiago: Gone
limburger: Gone
```

The first line is the result of calling asiago->eat(), which prints one message. The second line is the result of calling limburger->rot(), which prints another message.

The third line is simply the value in the variable CheeseCount. This variable was decremented once each time the computer called the OneMoreCheeseGone() function. Because the function was called twice, CheeseCount went from 2 to 1 to 0.

The final two lines show the contents of the status variable in the two objects. (The OneMoreCheeseGone() function had stored the string Gone in these variables.)

#### Listing 8-9 (continued)

```cpp
class Door
{
private:
    int HowManyInside;

public:
    void Start();
    void GoThrough(Cat *acat);
    void GoThrough(Dog *adog);
    void GoThrough(Human *ahuman);
};

void Door::Start()
{
    HowManyInside = 0;
}

void Door::GoThrough(Cat *somebody)
{
    cout << "Welcome, " << somebody->name << endl;
    cout << "A cat just entered!" << endl;
    HowManyInside++;
}

void Door::GoThrough(Dog *somebody)
{
    cout << "Welcome, " << somebody->name << endl;
    cout << "A dog just entered!" << endl;
    HowManyInside++;
}

void Door::GoThrough(Human *somebody)
{
    cout << "Welcome, " << somebody->name << endl;
    cout << "A human just entered!" << endl;
    HowManyInside++;
}

int main()
{
    Door entrance;
    entrance.Start();

    Cat *SneekyGirl = new Cat;
    SneekyGirl->name = "Sneeky Girl";

    Dog *LittleGeorge = new Dog;
    LittleGeorge->name = "Little George";

    Human *me = new Human;
    me->name = "Jeff";

    entrance.GoThrough(SneekyGirl);
    entrance.GoThrough(LittleGeorge);
    entrance.GoThrough(me);

    delete SneekyGirl;
    delete LittleGeorge;
    delete me;

    return 0;
}
```

The application allows them to enter like humans. The beginning of this application declares three classes, Cat, Dog, and Human, each with a name member. Next is the Door class. A private member, HowManyInside, tracks how many beings have entered. Then we have a public function called `Start()`, which activates the door. Finally, the class contains the overloaded functions. They all have the same name and the same return type. You can have different return types, but they must differ by parameters. These do; one takes a Cat pointer, one takes a Dog pointer; and one takes a Human pointer.

Next is the code for the member functions. The first function, `Start()`, is easy to activate. It sets HowManyInside to 0. The next three functions are overloaded. They do similar things, but they write slightly different messages. Each takes a different type.

Then we have `main()`, which creates a Door instance. We didn't make this a pointer (just to show that you can mix pointers with stack variables in an application). After creating the Door instance, we called its `Start()` function. Next, we created three creature instances: one Cat, one Dog, and one Human. We also set the name member variables for each.

Then we call the `entrance.GoThrough()` function. The first time we pass a Cat, then we pass a Dog, and then we pass a Human. (Sounds painful.) Because you can see the Door class, you know that we're calling three different functions that happened to be all named the same. But when we're *using* the class, we consider them all one function that happens to accept a Cat, a Dog, or a Human. That's the goal of overloading: to create what feels like *versions* of the one function.

### Starting and Ending with Constructors and Destructors

#### Starting with constructors

When you create a new instance of a class, you may want to do some basic setup on the object. Suppose you have a class called Apartment, with a private member variable called NumberOfOccupants and a member function called ComeOnIn(). The code for ComeOnIn() adds 1 to NumberOfOccupants.

When you create a new instance of `Apartment`, you probably want to start `NumberOfOccupants` at 0. The best way to do this is by adding a special member function, a *constructor*, to your class. This member function has a line of code such as

```cpp
NumberOfOccupants = 0;
```

Whenever you create a new instance of the class `Apartment`, the computer first calls this constructor for your new object, thereby setting `NumberOfOccupants` to 0.

Think of the constructor as an *initialization function*: The computer calls it when you create a new object.

To write a constructor, you add it as another member function to your class, and you make it public. You name the constructor the same as your class. For the class `Apartment`, we would name our constructor `Apartment()`. The constructor has no return type, not even `void`. You can have parameters in a constructor; see "Adding parameters to constructors," later in this chapter.

Listing 8-10, later in this section, shows a sample constructor along with a *destructor*, which we cover in the next section.

#### Ending with destructors

When you delete an instance of a class, you might want some *cleanup* code to straighten things out before the object goes off to the classroom in the sky. For example, your object may have member variables that are pointers to other objects. You may want to delete those other objects.

You put cleanup code in a special function called a destructor. A *destructor* is a finalization function that the computer calls before it deletes your object.

The destructor function gets the same name as the class, except it has a tilde, `~`, at the beginning of it. (The tilde is usually in the upper-left corner of the keyboard.) For a class called `Squirrel`, the destructor would be `~Squirrel()`. The destructor does not have a return type, not even `void`, because you can't return anything from a destructor (the object is gone, after all). You just start with the function name and no parameters.

![](img/6ba99460b0feb3585671a4612ff5fabb_219_0.png)

The next section, "Sampling constructors and destructors," shows an example that uses both constructors and destructors.

Constructors and destructors are a way of life for C++ programmers. Nearly every class has a constructor, and many also have a destructor.
