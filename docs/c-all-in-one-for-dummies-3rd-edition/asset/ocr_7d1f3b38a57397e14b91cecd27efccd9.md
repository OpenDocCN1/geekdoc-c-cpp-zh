```
```cpp
public:
    FrozenFood(int APrice, int AWeight);
    int GetPrice();
    int GetWeight();
    virtual void BakeChemistry();
};

class FrozenPizza : public FrozenFood
protected:
    int ADiameter;

public:
    FrozenPizza(int APrice, int AWeight, int ADiameter);
    void DumpInfo();
    void BakeChemistry();
};
```
```

You can see that we put the word virtual in the FrozenFood class, and then we put the function declaration again in the FrozenPizza class. Now, here are the BakeChemistry() functions:

```
```cpp
void FrozenFood::BakeChemistry()
{
    cout << "Baking, baking, baking!" << endl;
}
```
```

```
```cpp
void FrozenPizza::BakeChemistry()
{
    cout << "I'm getting crispy!" << endl;
}
```
```

Note that we did not put the word virtual in front of the functions; that only goes in the class declaration. Now, whenever you make an instance of each class and call BakeChemistry() for each instance, you call the one for the given class. Consider the following two lines of code:

```
```cpp
FrozenPizza pepperoni(450, 12, 14);
pepperoni.BakeChemistry();
```
```

Because pepperoni is an instance of FrozenPizza, this code calls the BakeChemistry() for the FrozenPizza class, not for the FrozenFood class.

You may not want any code in your base class for the BakeChemistry() function. If so, you can do this:

```
```cpp
virtual void BakeChemistry() {}
```
```

Wait! Why would you want a function that has no code? Well, we’re not as goofy as we look. Okay, we are goofy. But regardless, you may not want any code here, but you do want code in the derived classes, and you want them to be different versions of the same code. The idea then is to provide a basic, default set of code that the classes inherit if they don’t override the function. And sometimes, that basic, default set of code is simply nothing. And so you would only put an open brace and a closing brace, and you can do that inside the class itself: