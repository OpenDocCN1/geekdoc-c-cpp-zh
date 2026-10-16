for a class named Critter. To define a class, start with the keyword class, followed by the class name. By convention, class names begin with an uppercase letter. You surround the class body with curly braces and end it with a semicolon.

# Declaring Data Members

In a class definition, you can declare class data members to represent object qualities. I give the critters just one quality, hunger. I see hunger as a range that could be represented by an integer, so I declare an int data member m_Hunger.

```
int m_Hunger;      // data member
```

This means that every Critter object will have its own hunger level, represented by its own data member named m_Hunger. Notice that I prefix the data member name with m_. Some game programmers follow this naming convention so that data members are instantly recognizable.

# Declaring Member Functions

In a class definition, you can also declare member functions to represent object abilities. I give a critter just one—the ability to greet the world and announce its hunger level—by declaring the member function Greet().

```
void Greet();      // member function prototype
```

This means that every Critter object will have the ability to say hi and announce its own hunger level through its member function, Greet(). By convention, member function names begin with an uppercase letter. At this point, I’ve only declared the member function Greet(). Don’t worry, though, I’ll define it outside of the class.

# Hint

> You might have noticed the keyword public in the class definition. You can ignore it for now. You’ll learn more about it a bit later in this chapter, in the section, “Specifying Public and Private Access Levels.”

# Defining Member Functions

You can define member functions outside of a class definition. Outside of the Critter class definition, I define the Critter member function Greet(), which says hi and displays the critter’s hunger level.