> Hint
> Being able to call a base class constructor is useful when you want to pass specific values to it.

# Declaring Virtual Base Class Member Functions

Any inherited base class member function that you expect to be overridden in a derived class should be declared as virtual, using the keyword virtual. When you declare a member function virtual, you provide a way for overridden versions of the member function to work as expected with pointers and references to objects. Since I know that I'll override Taunt() in the derived class, Boss, I declare Taunt() virtual in my base class, Enemy.

```
void virtual Taunt() const;    //made virtual to be overridden
```

> Trap
> Although you can override non-virtual member functions, this can lead to behavior you might not expect. A good rule of thumb is to declare any base class member function to be overridden as virtual.

Outside the Enemy class definition, I define Taunt():

```
void Enemy::Taunt() const
{
    cout << "The enemy says he will fight you.\n";
}
```

Notice that I didn't use the keyword virtual in the definition. You don't use virtual in the definition of a member function, only in its declaration.

Once a member function has been declared virtual, it's virtual in any derived class. This means you don't have to use the keyword virtual in a declaration when you override a virtual member function, but you should use it anyway because it will remind you that the function is indeed virtual. So, when I override Taunt() in Boss, I explicitly declare it as virtual, even though I don't have to:

```
void virtual Taunt() const;    //optional use of keyword virtual
```

# Overriding Virtual Base Class Member Functions

The next step in overriding is to give the member function a new definition in the derived class. That's what I do for the Boss class with:

```
void Boss::Taunt() const    //override base class member function
```