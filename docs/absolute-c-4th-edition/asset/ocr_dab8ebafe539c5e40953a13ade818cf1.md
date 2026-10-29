On the other hand, both the class Employee and the class HourlyEmployee define a function with the following function declaration:

```
void printCheck( );
```

In this case, the class HourlyEmployee has only one function named printCheck, but the definition of the function printCheck for the class HourlyEmployee is different from its definition for the class Employee. In this case, the function printCheck has been redefined.

If you get redefining and overloading confused, you do have one consolation: They are both legal. So, it is more important to learn how to use them than it is to learn to distinguish between them. Nonetheless, you should learn the difference between them.

# SIGNATURE

A function’s signature is the function’s name with the sequence of types in the parameter list, not including the const keyword and the ampersand, &. When you overload a function name, the two definitions of the function name must have different signatures using this definition of signature. (Some authorities include the const and/or ampersand as part of the signature, but we wanted a definition that works for explaining overloading.) A function that has the same name in a derived class as in the base class but has a different signature is overloaded, not redefined.

(As we noted in Chapter 4, some compilers will, in fact, allow you to overload on the basis of const versus no const, but you should not count on this. The C++ standard says it is not allowed.)

# ACCESS TO A REDEFINED BASE FUNCTION

Suppose you redefine a function so that it has a different definition in the derived class from what it had in the base class. The definition that was given in the base class is not completely lost to the derived class objects. However, if you want to invoke the version of the function given in the base class with an object in the derived class, you need some way to say “use the definition of this function as given in the base class (even though I am an object of the derived class).” The way you say this is to use the scope resolution operator with the name of the base class. An example should clarify the details.

Consider the base class Employee (Display 14.1) and the derived class HourlyEmployee (Display 14.3). The function printCheck( ) is defined in both classes. Now suppose you have an object of each class, as in the following:

```
Employee JaneE;
HourlyEmployee SallyH;
```

Then

```
JaneE.printCheck( );
```