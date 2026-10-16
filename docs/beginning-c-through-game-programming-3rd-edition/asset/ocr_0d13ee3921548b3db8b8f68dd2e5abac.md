For the copy constructor, you also usually want to call the copy constructor from a base class, which you can call just like any base class constructor. If Boss is derived from Enemy, the copy constructor defined in Boss could start:

```
Boss (const Boss& b): Enemy(b)  //handles the data members inherited from Enemy
{
    //now take care of data members defined in Boss
```

By calling Enemy’s copy constructor with Enemy(b), you copy that Enemy’s data members into the new Boss object. In the remainder of Boss’ copy constructor, you can take care of copying the data members declared in Boss into the new object.

# INTRODUCING POLYMORPHISM

One of the pillars of OOP is polymorphism, which means that a member function will produce different results depending on the type of object for which it is being called. For example, suppose you have a group of bad guys that the player is facing, and the group is made of objects of different types that are related through inheritance, such as enemies and bosses. Through the magic of polymorphism, you could call the same member function for each bad guy in the group, say to attack the player, and the type of each object would determine the exact results. The call for the enemy objects could produce one result, such as a weak attack, while the call for bosses could produce a different result, such as a powerful attack. This might sound a lot like overriding, but polymorphism is different because the effect of the function call is dynamic and is determined at run time, depending on the object type. But the best way to understand this isn’t through theoretical discussion; it is through a concrete example.

# Introducing the Polymorphic Bad Guy Program

The Polymorphic Bad Guy program demonstrates how to achieve polymorphic behavior. It shows what happens when you use a pointer to a base class to call inherited virtual member functions. It also shows how using virtual destructors ensures that the correct destructors are called for objects pointed to by pointers to a base class. Figure 10.4 shows the results of the program.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 10 folder; the filename is polymorphic_bad_guy.cpp.