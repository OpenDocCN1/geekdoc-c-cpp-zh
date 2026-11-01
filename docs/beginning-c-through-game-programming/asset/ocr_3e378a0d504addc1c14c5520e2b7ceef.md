The function overloads the << operator so that when I send a Critter object with the << to cout, the data member m_Name is displayed. Essentially, the function allows me to easily display Critter objects. The function can directly access the private data member m_Name of a Critter object because I made the function a friend of the Critter class with the following line in Critter:

```
friend ostream& operator<<(ostream& os, const Critter& aCritter);
```

This means I can simply display a Critter object by sending it to cout with the << operator, which is what I do in main() with the following line, which displays the text Critter Object - m_Name: Poochie.

```
cout << crit;
```

> **Hint**
> 
> With all the tools and debugging options available to game programmers, sometimes simply displaying the values of variables is the best way to understand what's happening in your programs. Overloading the << operator can help you do that.

This function works because cout is of the type ostream, which already overloads the << operator so that you can send built-in types to cout.

# DYNAMICALLY ALLOCATING MEMORY

So far, whenever you've declared a variable, C++ has allocated the necessary memory for it. When the function that the variable was created in ended, C++ freed the memory. This memory, which is used for local variables, is called the stack. But there's another kind of memory that persists independent of the functions in a program. You, the programmer, are in charge of allocating and freeing this memory, collectively called the heap (or free store).

At this point, you might be thinking, "Why bother with another type of memory? The stack works just fine, thank you." Using the dynamic memory of the heap offers great benefits that can be summed up in one word: efficiency. By using the heap, you can use only the amount of memory you need at any given time. If you have a game with a level that has 100 enemies, you can allocate the memory for the enemies at the beginning of the level and free the memory at the end. The heap also allows you to create an object in one function that you can access even after that function ends (without having to return a copy of the