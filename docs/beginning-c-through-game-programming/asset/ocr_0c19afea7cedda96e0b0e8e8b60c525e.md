version, it's as if I've extended the definition of what it means for a boss to attack. What I'm essentially saying is that when a boss attacks, the boss does exactly what an enemy does and then laughs. When I call the member function for a Boss object in main() with the following line, Boss' Attack() member function is called because I've overloaded Attack().

```
aBoss.Attack();
```

The first thing that Boss' Attack() member function does is explicitly call Enemy's Attack() member function, which displays the message Attack! Inflicts 30 damage points. Then, Boss' Attack() member function displays the message And laughs heartily at you.

# Trick

You can extend the way a member function of a base class works in a derived class by overriding the base class method and then explicitly calling the base class member function from this new definition in the derived class and adding some functionality.

# USING OVERLOADED ASSIGNMENT OPERATORS AND COPY CONSTRUCTORS IN DERIVED CLASSES

You already know how to write an overloaded assignment operator and a copy constructor for a class. However, writing them for a derived class requires a little bit more work because they aren't inherited from a base class.

When you overload the assignment operator in a derived class, you usually want to call the assignment operator member function from the base class, which you can explicitly call using the base class name as a prefix. If Boss is derived from Enemy, the overloaded assignment operator member function defined in Boss could start:

```
Boss& operator=(const Boss& b)
{
    Enemy::operator=(b);    //handles the data members inherited from Enemy
    //now take care of data members defined in Boss
}
```

The explicit call to Enemy's assignment operator member function handles the data members inherited from Enemy. The rest of the member function would take care of the data members defined in Boss.