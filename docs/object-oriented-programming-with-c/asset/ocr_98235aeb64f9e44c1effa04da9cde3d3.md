derived class. It is incremented or decremented only relative to its base type. Therefore, we should not use this method to move the pointer to the next object.

+   10. If a virtual function is defined in the base class, it need not be necessarily redefined in the derived class. In such cases, calls will invoke the base function.

# 9.7 Pure Virtual Functions

It is normal practice to declare a function virtual inside the base class and redefine it in the derived classes. The function inside the base class is seldom used for performing any task. It only serves as a *placeholder*. For example, we have not defined any object of class media and therefore the function display() in the base class has been defined ‘empty’. Such functions are called “do-nothing” functions.

A “do-nothing” function may be defined as follows:

```
virtual void display() = 0;
```

Such functions are called *pure virtual* functions. **A pure virtual function is a function declared in a base class that has no definition relative to the base class.** In such cases, the compiler requires each derived class to either define the function or redeclare it as a pure virtual function. Remember that a class containing pure virtual functions cannot be used to declare any objects of its own. As stated earlier, such classes are called *abstract base classes*. The main objective of an abstract base class is to provide some traits to the derived classes and to create a base pointer required for achieving run time polymorphism.

Program 9.14 demonstrates the use of pure virtual function: