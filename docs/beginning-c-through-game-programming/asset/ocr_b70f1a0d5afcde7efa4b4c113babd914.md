called and the text A boss attacks and inflicts 30 damage points. being displayed on the screen.

```
pBadGuy->Attack();
```

# Hint

Virtual functions produce polymorphic behavior through references as well as through pointers.

# Trap

If you override a non-virtual member function in a derived class and call that member function on a derived class object through a pointer to a base class, you'll get the results of the base class member function and not the derived class member function definition. This is easier to understand with an example. If in the Polymorphic Bad Guy program I hadn't declared Attack() as virtual, then when I invoked the member function through a pointer to Enemy on a Boss object with pBadGuy->Attack();, I would have gotten the message An enemy attacks and inflicts 10 damage points. This would have happened as a result of early binding, in which the exact member function is bound based on the pointer type—in this case, Enemy. But because Attack() is declared as virtual, the member function call is based on the type of object being pointed to at run time, Boss in this case, not fixed by pointer type. I achieve this polymorphic behavior as the result of late binding because Attack() is virtual. The moral of the story is that you should only override virtual member functions.

# Trap

The benefits of virtual functions aren't free; there is a performance cost associated with the overhead. Therefore, you should use virtual functions only when you need them.

# Defining Virtual Destructors

When you use a pointer to a base class to point to an object of a derived class, you have a potential problem. When you delete the pointer, only the base class' destructor will be called for the object. This could lead to disastrous results because the derived class' destructor might need to free memory (as the destructor for Boss does). The solution, as you might have guessed, is to make the base class' destructor virtual. That way, the derived class' destructor is called, which (as always) leads to the calling the base class' destructor, giving every class the chance to clean up after itself. I put this theory into action when I declare Enemy's destructor virtual.

```
virtual ~Enemy();
```