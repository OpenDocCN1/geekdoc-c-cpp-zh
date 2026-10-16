
To derive classes of your own, follow my example. After the class name in a class definition, put a colon followed by an access modifier (such as `public`), followed by the name of the base class. It’s perfectly acceptable to derive a new class from a derived class, and sometimes it makes perfect sense to do so. However, to keep things simple, I’m only going to deal with one level of inheritance in this example.

There are actually a few base class member functions that are not inherited by derived classes. They are as follows:

- Constructors
- Copy constructors
- Destructors
- Overloaded assignment operators

You have to write your own versions of these in the derived class.

## Instantiating Objects from a Derived Class

In `main()`, I instantiate an Enemy object and then call its `Attack()` member function. This works just as you’d expect. The interesting part of the program begins next, when I instantiate a Boss object.

```
Boss boss1;
```

After this line of code, I have a `Boss` object with an `m_Damage` data member equal to 10 and an `m_DamageMultiplier` data member equal to 3. How did this happen? Although constructors and destructors are not inherited from a base class, they are called when an instance is created or destroyed. In fact, a base class constructor is called before the derived class constructor to create its part of the final object.

In this case, when a `Boss` object is instantiated, the default `Enemy` constructor is automatically called and the object gets an `m_Damage` data member with a value of 10 (just like any `Enemy` object would). Then, the `Boss` constructor is called and finishes off the object by giving it an `m_DamageMultiplier` data member with a value of 3. The reverse happens when a `Boss` object is destroyed at the end of the program. First, the `Boss` class destructor is called for the object, and then the Enemy class destructor is called. Because I didn’t define destructors in this program, nothing special happens before the `Boss` object ceases to exist.

### Hint

> The fact that base class destructors are called for objects of derived classes ensures that each class gets its chance to clean up any part of the object that needs to be taken care of, such as memory on the heap.

## Using Inherited Members

Next, I call an inherited member function of the `Boss` object, which displays the exact same message as `enemy1.Attack()`.

```
boss1.Attack();
```

That makes perfect sense because the same code is being executed and both objects have an `m_Damage` data member equal to 10. Notice that the function call looks the same as it did for `enemy1`. The fact that `Boss` inherited the member function from `Enemy` makes no difference in how the function is called.

Next, I get `Boss` to pull out its special attack, which displays the message `Special Attack inflicts 30 damage points!`

```
boss1.SpecialAttack();
```

The thing to notice about this is that `SpecialAttack()`, declared as a part of `Boss`, uses the data member `m_Damage`, declared in `Enemy`. That’s perfectly fine. `Boss` inherits `m_Damage` from `Enemy` and, in this example, the data member works like any other data member in the `Boss` class.

## CONTROLLING ACCESS UNDER INHERITANCE

When you derive one class from another, you can control how much access the derived class has to the base class’ members. For the same reasons that you want to provide only as much access as is necessary to a class’ members to the rest of your program, you want to provide only as much access as is necessary to a class’ members to a derived class. Not coincidentally, you use the same access modifiers that you’ve seen before—public, protected, and private. (Okay, you haven’t seen protected before, but I’ll explain that modifier in the “Using Access Modifiers with Class Members” section.)

## Introducing the Simple Boss 2.0 Program

The Simple Boss 2.0 program is another version of the Simple Boss program from earlier in this chapter. The new version, Simple Boss 2.0, looks exactly the same to the user, but the code is a little different because I put some restrictions on base class members. If you want to see what the program does, take a look back at Figure 10.2.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 10 folder; the filename is simple_boss2.cpp.

```
//Simple Boss 2.0
//Demonstrates access control under inheritance

#include <iostream>
using namespace std;

class Enemy
{
public:
    Enemy();
    void Attack() const;

protected:
    int m_Damage;
};

Enemy::Enemy():
    m_Damage(10)
{}

void Enemy::Attack() const
{
    cout << "Attack inflicts " << m_Damage << " damage points!\n";
}

class Boss : public Enemy
{
public:
    Boss();
    void SpecialAttack() const;

private:
    int m_DamageMultiplier;
};

Boss::Boss():
    m_DamageMultiplier(3)
{}

void Boss::SpecialAttack() const
{
    cout << "Special Attack inflicts " << (m_DamageMultiplier * m_Damage);
    cout << " damage points!\n";
}

int main()
{
    cout << "Creating an enemy.\n";
    Enemy enemy1;
    enemy1.Attack();

    cout << "\nCreating a boss.\n";
    Boss boss1;
    boss1.Attack();
    boss1.SpecialAttack();

    return 0;
}
```

## Using Access Modifiers with Class Members

You’ve seen the access modifiers public and private used with class members before, but there’s a third modifier you can use with members of a class—protected. That’s what I use with the data member of Enemy.

```
protected:
    int m_Damage;
```

Members that are specified as protected are not accessible outside of the class, except in some cases of inheritance. As a refresher, here are the three levels of member access:

- public members are accessible to all code in a program.
- `protected` members are accessible only in their own class and certain derived classes, depending upon the access level used in inheritance.
- `private` members are only accessible in their own class, which means they are not directly accessible in any derived class.

## Using Access Modifiers When Deriving Classes

When you derive a class from an existing one, you can use an access modifier, such as `public`, which I used in deriving `Boss`.

```
class Boss : public Enemy
```

Using public derivation means that public members in the base class become public members in the derived class, protected members in the base class become protected members in the derived class, and private members in the base class are inaccessible in the derived class.

### Trick

> Even if base data members are private, you can still use them indirectly through base class member functions. You can even get and set their values if the base class has accessor member functions.

Because `Boss` inherits from `Enemy` using the keyword `public`, `Boss` inherits `Enemy`’s public member functions as public member functions. It also means that `Boss` inherits `m_Damage` as a protected data member. The class essentially acts as if I simply copied and pasted the code for these two `Enemy` class members right into the `Boss` definition. But through the beauty of inheritance, I didn’t have to do this. The upshot is that the `Boss` class can access `Attack()` and `m_Damage()`.

### Hint

> You can derive a new class with the `protected` and `private` keywords, but they’re rarely used and are beyond the scope of this book.

## CALLING AND OVERRIDING BASE CLASS MEMBER FUNCTIONS

You’re not stuck with every base class member function you inherit in a derived class as is. You have options that allow you to customize how those inherited member functions work in your derived class. You can override them by giving them new definitions in your derived class. You can also explicitly call a base class member function from any member function of your derived class.

## Introducing the Overriding Boss Program

The Overriding Boss program demonstrates calling and overriding base class member functions in a derived class. The program creates an enemy that taunts the player and then attacks him. Next, the program creates a boss from a derived class. The boss also taunts the player and attacks him, but the interesting thing is that the inherited behaviors of taunting and attacking are changed for the boss (who is a bit cockier than the enemy). These changes are accomplished through function overriding and calling a base class member function. Figure 10.3 shows the results of the program.

![](img/34f09be0ed6217c465debc4490197d4f_363_0.png)

Figure 10.3
The Boss class inherits and overrides the base class member functions Taunt() and Attack(), creating new behaviors for the functions in Boss.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 10 folder; the filename is overriding_boss.cpp.

```
//Overriding Boss
//Demonstrates calling and overriding base member functions

#include <iostream>

using namespace std;
```
