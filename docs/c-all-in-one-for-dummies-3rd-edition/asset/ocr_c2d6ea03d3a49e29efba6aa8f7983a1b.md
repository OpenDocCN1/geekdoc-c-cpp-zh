To override the abstract virtual function, you override as you would with any virtual function. This class includes a function that overrides the `BakeChemistry()` function:

```
```cpp
class FrozenPizza : public FrozenFood
{
protected:
    int Diameter;

public:
    FrozenPizza(int APrice, int AWeight, int ADiameter);
    void DumpInfo();
    void BakeChemistry();
};
```
```

Then you provide the code for the `BakeChemistry()` function, as in

```
```cpp
void FrozenPizza::BakeChemistry()
{
    cout << "I'm getting crispy under this heat!" << endl;
}
```
```

There's nothing magical about defining the override function, but you are *required* to override it if you want to create an instance of this class.

# ## Discovering Classes

In your studies of object-oriented programming, you could spend weeks and weeks searching for the answer to this question: How do you know what classes to put in your application? Oddly, many of the books on object-oriented programming don't even tackle this question. Too many people, even self-proclaimed experts, simply don't know the answer to this question.

In this section, we show you how to discover the classes you need for your project, and we put the concepts in the context of the bigger picture of software engineering.

# ### Engineering your software

Ready to write your application? Okay, sit down and start coding. And call us in six months. Oh, and in case we forgot to mention, this software that you build has to do exactly what we, your customers, need. And please, please, don't let it mess up, okay?

Well now, isn't that nice? How are you supposed to know what we need, and much less, how are you supposed to get it perfect the first time? Yet, believe it or not, many young programmers build their software this way. The shoot-from-the-hip approach goes something like this:

+   1. "Hey! I have a *really* great idea!"
+   2. Open up the compiler.