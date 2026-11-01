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

# Using Base Class Pointers to Derived Class Objects

An object of a derived class is also a member of the base class. For example, in the Polymorphic Bad Guy program, a Boss object is an Enemy object, too. That makes sense because a Boss is really only a specialized kind of enemy. It also makes sense because a Boss object has all of the members of an Enemy object. Okay, so what? Well, because an object of a derived class is also a member of the base class, you can use a pointer to the base class to point to an object of the derived class. That's what I do in main() with the following line, which instantiates a Boss object on the heap and creates a pointer to Enemy, pBadGuy, that points to the Boss object.

```
Enemy* pBadGuy = new Boss();
```

Why in the world would you want to do this? It's useful because it allows you to deal with objects without requiring that you know their exact type. For example, you could have a function that accepts a pointer to Enemy that could work with either an Enemy or a Boss object. The function wouldn't have to know the exact type of object being passed to it; it could work with the object to produce different results depending on the object's type, as long as derived member functions were declared virtual. Because Attack() is virtual, the correct version of the member function will be called (based on the type of object) and will not be fixed by the type of pointer.

I prove that the behavior will be polymorphic in main(). Remember that pBadGuy is a pointer to Enemy that points to a Boss object. So, the following line calls the Attack() member function of a Boss object through a pointer to Enemy, which correctly results in the Attack() member function defined in Boss being