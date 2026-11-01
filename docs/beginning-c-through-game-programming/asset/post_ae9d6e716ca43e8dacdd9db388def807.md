
For the copy constructor, you also usually want to call the copy constructor from a base class, which you can call just like any base class constructor. If Boss is derived from Enemy, the copy constructor defined in Boss could start:

```cpp
Boss::Boss(const Boss& b): Enemy(b) //handles the data members inherited from Enemy
{
    //now take care of data members defined in Boss
}
```

By calling Enemy's copy constructor with Enemy(b), you copy that Enemy's data members into the new Boss object. In the remainder of Boss' copy constructor, you can take care of copying the data members declared in Boss into the new object.

## INTRODUCING POLYMORPHISM

One of the pillars of OOP is polymorphism, which means that a member function will produce different results depending on the type of object for which it is being called. For example, suppose you have a group of bad guys that the player is facing, and the group is made of objects of different types that are related through inheritance, such as enemies and bosses. Through the magic of polymorphism, you could call the same member function for each bad guy in the group, say to attack the player, and the type of each object would determine the exact results. The call for the enemy objects could produce one result, such as a weak attack, while the call for bosses could produce a different result, such as a powerful attack. This might sound a lot like overriding, but polymorphism is different because the effect of the function call is dynamic and is determined at run time, depending on the object type. But the best way to understand this isn't through theoretical discussion; it is through a concrete example.

### Introducing the Polymorphic Bad Guy Program

The Polymorphic Bad Guy program demonstrates how to achieve polymorphic behavior. It shows what happens when you use a pointer to a base class to call inherited virtual member functions. It also shows how using virtual destructors ensures that the correct destructors are called for objects pointed to by pointers to a base class. Figure 10.4 shows the results of the program.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 10 folder; the filename is polymorphic_bad_guy.cpp.

```
Enemy::~Enemy()
{
    cout << "In Enemy destructor, deleting m_pDamage.\n";
    delete m_pDamage;
    m_pDamage = 0;
}

void Enemy::Attack() const
{
    cout << "An enemy attacks and inflicts " << *m_pDamage << " damage points.";
}

class Boss : public Enemy
{
public:
    Boss(int multiplier = 3);
    virtual ~Boss();
    virtual void Attack() const;

protected:
    int* m_pMultiplier;
};

Boss::Boss(int multiplier)
{
    m_pMultiplier = new int(multiplier);
}

Boss::~Boss()
{
    cout << "In Boss destructor, deleting m_pMultiplier.\n";
    delete m_pMultiplier;
    m_pMultiplier = 0;
}

void Boss::Attack() const
{
    cout << "A boss attacks and inflicts " << (*m_pDamage) * (*m_pMultiplier)
         << " damage points.";
}
```

```
int main()
{
    cout << "Calling Attack() on Boss object through pointer to Enemy:\n";
    Enemy* pBadGuy = new Boss();
    pBadGuy->Attack();

    cout << "\n\nDeleting pointer to Enemy:\n";
    delete pBadGuy;
    pBadGuy = 0;

    return 0;
}
```

### Using Base Class Pointers to Derived Class Objects

An object of a derived class is also a member of the base class. For example, in the Polymorphic Bad Guy program, a Boss object is an Enemy object, too. That makes sense because a Boss is really only a specialized kind of enemy. It also makes sense because a Boss object has all of the members of an Enemy object. Okay, so what? Well, because an object of a derived class is also a member of the base class, you can use a pointer to the base class to point to an object of the derived class. That's what I do in main() with the following line, which instantiates a Boss object on the heap and creates a pointer to Enemy, pBadGuy, that points to the Boss object.

```
Enemy* pBadGuy = new Boss();
```

Why in the world would you want to do this? It's useful because it allows you to deal with objects without requiring that you know their exact type. For example, you could have a function that accepts a pointer to Enemy that could work with either an Enemy or a Boss object. The function wouldn't have to know the exact type of object being passed to it; it could work with the object to produce different results depending on the object's type, as long as derived member functions were declared virtual. Because Attack() is virtual, the correct version of the member function will be called (based on the type of object) and will not be fixed by the type of pointer.

I prove that the behavior will be polymorphic in main(). Remember that pBadGuy is a pointer to Enemy that points to a Boss object. So, the following line calls the Attack() member function of a Boss object through a pointer to Enemy, which correctly results in the Attack() member function defined in Boss being
called and the text A boss attacks and inflicts 30 damage points. being displayed on the screen.

```
pBadGuy->Attack();
```

### Hint

Virtual functions produce polymorphic behavior through references as well as through pointers.

### Trap

If you override a non-virtual member function in a derived class and call that member function on a derived class object through a pointer to a base class, you'll get the results of the base class member function and not the derived class member function definition. This is easier to understand with an example. If in the Polymorphic Bad Guy program I hadn't declared Attack() as virtual, then when I invoked the member function through a pointer to Enemy on a Boss object with pBadGuy->Attack();, I would have gotten the message An enemy attacks and inflicts 10 damage points. This would have happened as a result of early binding, in which the exact member function is bound based on the pointer type—in this case, Enemy. But because Attack() is declared as virtual, the member function call is based on the type of object being pointed to at run time, Boss in this case, not fixed by pointer type. I achieve this polymorphic behavior as the result of late binding because Attack() is virtual. The moral of the story is that you should only override virtual member functions.

### Trap

The benefits of virtual functions aren't free; there is a performance cost associated with the overhead. Therefore, you should use virtual functions only when you need them.

### Defining Virtual Destructors

When you use a pointer to a base class to point to an object of a derived class, you have a potential problem. When you delete the pointer, only the base class' destructor will be called for the object. This could lead to disastrous results because the derived class' destructor might need to free memory (as the destructor for Boss does). The solution, as you might have guessed, is to make the base class' destructor virtual. That way, the derived class' destructor is called, which (as always) leads to the calling the base class' destructor, giving every class the chance to clean up after itself. I put this theory into action when I declare Enemy's destructor virtual.

```
virtual ~Enemy();
```

![](img/c7e8651578bccd573227f684823b8754_375_0.png)

### Figure 10.5

The orc is an object instantiated from a class derived from an abstract class for all creatures.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 10 folder; the filename is abstract_creature.cpp.

```
//Abstract Creature
//Demonstrates abstract classes

#include <iostream>
using namespace std;

class Creature  //abstract class
{
public:
    Creature(int health =100);
    virtual void Greet() const = 0;   //pure virtual member function
    virtual void DisplayHealth() const;

protected:
    int m_Health;
};

Creature::Creature(int health):
    m_Health(health)
