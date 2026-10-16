# Creating Friend Functions

A friend function can access any member of a class of which it’s a friend. You specify that a function is a friend of a class by listing the function prototype preceded by the keyword friend inside the class definition. That’s what I do inside the Critter definition with the following line, which says that the global function Peek() is a friend of Critter.

```
friend void Peek(const Critter& aCritter);
```

This means Peek() can access any member of Critter even though it’s not a member function of the class. Peek() takes advantage of this relationship by accessing the private data member m_Name to display the name of a critter passed to the function.

```
void Peek(const Critter& aCritter)
{
    cout << aCritter.m_Name << endl;
}
```

When I call Peek() in main() with the following line, the private data member m_Name of crit is displayed and Poochie appears on the screen.

```
Peek(crit);
```

# Overloading Operators

Overloading operators might sound like something you want to avoid at all costs—as in, “Look out, that operator is overloaded and she’s about to blow!”—but it’s not. Operator overloading lets you give meaning to built-in operators used with new types that you define. For example, you could overload the * operator so that when it is used with two 3D matrices (objects instantiated from some class that you’ve defined), the result is the multiplication of the matrices.

To overload an operator, define a function called operatorX, where X is the operator you want to overload. That’s what I do when I overload the << operator; I define a function named operator<<.

```
ostream& operator<<(ostream& os, const Critter& aCritter)
{
    os << "Critter Object - ";
    os << "m_Name: " << aCritter.m_Name;
    return os;
}
```