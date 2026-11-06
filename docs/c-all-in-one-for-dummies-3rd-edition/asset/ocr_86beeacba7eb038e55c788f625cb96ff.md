Sometimes you may want an object to hold an instance of another class but want to keep the instance around after you delete the containing object. In that case, you wouldn’t delete the other instance in the destructor.

Here’s a modification to the Container class (found in the Destructor02 example) that deletes the second instance:

```
```cpp
class Container
{
public:
    LittleInst first;
    LittleInst *second;
    Container();
    ~Container() { delete second; }
};
```
```

Then, when you run these two lines again

```
```cpp
Container *inst = new Container;
Delete inst;
```
```

you see this output, which deletes both instances:

```
```
2
1
```
```

In the preceding output, you can see that it deleted the second instance first. The reason is that the application calls the destructor before it destroys the direct members. In this case, when we deleted our Container instance, the application first called our destructor before deleting our first member. That’s actually a good idea, because in the code for our destructor, we may want to do some work on our member variables before they get wiped out.

# ### *Virtually inheriting destructors*

You can (and should) make destructors virtual — unlike constructors. The reason is that you can pass an instance of a derived class into a function that takes a base class, like this:

```
```cpp
void ProcessAndDelete(DeleteMe *inst)
{
    cout << inst->Number << endl;
    delete inst;
}
```
```

This function takes an instance of class DeleteMe, does some work on it, and deletes it. Now, suppose you have a class derived from DeleteMe, say class Derived. Because of the rules of inheritance, you’re allowed to pass the instance of Derived into this function. But by the rules of *polymorphism* (as described in the “Specializing with polymorphism” section of

Book IV  
Chapter 3  
Constructors and Destructors and Exceptions