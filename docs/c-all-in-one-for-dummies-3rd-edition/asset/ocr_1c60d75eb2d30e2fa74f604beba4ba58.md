```
class Dad
{
public:
    int Bagel;
    void Beauty()
    {
        cout << "I'm beautiful!" << endl;
    }
};

class Derived : public Mom, public Dad
{
};
```

In the preceding code, each of the two base classes, Mom and Dad, has a Bagel member. The compiler will let you do this. But if you try to access the member as in the following code, you get an error:

```
Derived child;
child.Bagel = 42;
```

Here’s the error message we see in Code::Blocks:

```
error: request for member 'Bagel' is ambiguous
```

Aha! We’re being *ambiguous*! It means the compiler isn’t sure which Bagel we’re referring to: The one inherited from Mom or the one inherited from Dad. If you write code like this, make sure you know which inherited member you’re referring to. Now this is going to look bizarre, but we promise that it’s correct. Suppose we’re referring to the Bagel inherited from Mom. Then we can put the name Mom before the word Bagel, separated by two colons:

```
child.Mom::Bagel = 42;
```

Yes, that really is correct, even though it seems a little strange. And if we want to refer to the one by Dad, we do this:

```
child.Dad::Bagel = 17;
```

Both lines compile properly because we’re removing any ambiguities.

When you use multiple inheritance, remove any ambiguities by specifying the name of the base class. But don’t worry if you forget: The compiler will give you an error message because it won’t know which item you’re referring to.

![](bbox=[0.143, 0.734, 0.229, 0.804])

# Virtual inheritance

At times, you may see the word *virtual* thrown in when deriving a new class, as in the following:

```
class Diamond : virtual public Rock
```