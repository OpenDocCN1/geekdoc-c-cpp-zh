```
{
    cout << "The boss says he will end your pitiful existence.\n";
}
```

This new definition is executed when I call the member function through any Boss object. It replaces the definition of Taunt() inherited from Enemy for all Boss objects. When I call the member function in main() with the following line, the message The boss says he will end your pitiful existence. is displayed.

aBoss.Taunt();

Overriding member functions is useful when you want to change or extend the behavior of base class member functions in derived classes.

# Trap

> Don't confuse override with overload. When you override a member function, you provide a new definition of it in a derived class. When you overload a function, you create multiple versions of it with different signatures.

# Trap

> When you override an overloaded base class member function, you hide all of the other overloaded versions of the base class member function—meaning that the only way to access the other versions of the member function is to explicitly call the base class member function. So if you override an overloaded member function, it's a good idea to override every version of the overloaded function.

# Calling Base Class Member Functions

You can directly call a base class member function from any function in a derived class. All you have to do is prefix the class name to the member function name with the scope resolution operator. That's what I do when I define the overridden version of Attack() for the Boss class.

```
void Boss::Attack() const    //override base class member function
{
    Enemy::Attack();           //call base class member function
    cout << " And laughs heartily at you.\n";
}
```

The code Enemy::Attack(); explicitly calls the Attack() member function of Enemy. Because the Attack() definition in Boss overrides the class' inherited