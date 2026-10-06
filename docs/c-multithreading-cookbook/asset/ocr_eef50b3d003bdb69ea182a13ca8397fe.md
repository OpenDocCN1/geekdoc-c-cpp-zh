# Introduction to C++ Concepts and Features

Each of these three classes has the same method names but different implementations, similar to overriding but different in meaning. How? Well, if you look at the main function, you'll notice that we declared an array of pointers of CFigure. As a pointer or reference to a base class can always point to any of its derived classes, it is possible to create an object of CTriangle and set the CFigure pointer to point at it, using the following code:

```
figures[0] = new CTriangle(2.1, 3.2, 4.3);
```

In the same way, we create other figures using the following code:

```
figures[1] = new CSquare(5.4, 6.5);
figures[2] = new CCircle(8. 8);
```

Now, refer to the following

```
for (int i = 0; i < 3; i++)
{
  cout << "Figure:\t" << figures[i]->GetType() ()
  << "\nCircumference:\t" << figures[i]->Circumference ()
  << "\nArea:\t" << figures[i]->Area () << endl;
}
```

compiler will use a C++ feature called dynamic binding to resolve the type of object to which the figure points. It'll then call an appropriate virtual method. Dynamic binding is possible only if the method is declared virtually and you access it via a pointer or reference.

Let's go back to the example with persons. We have to declare objects of type cPerson, cWorker, and cStudent. All three are of different types, and you can call the WhoAMi method, for example, by using the following code:

```
cPerson.WhoAMi()
```

The compiler knows that you are referring to the cPerson object, which is of CPerson type, and is method. On the other hand, in the example with, the compiler doesn't know what type of object the figure pointer will point to during compilation. This is why it is called dynamic binding.

# Event handlers and Message Passing Interface

Many programs respond to events, such as when a user presses a button or inputs some text. A very important mechanism is event handling or the ability of a program to react to user action. If we want to handle when a user presses a button, we need to create some kind of a listener that will listen to button clicks, in this case a process.