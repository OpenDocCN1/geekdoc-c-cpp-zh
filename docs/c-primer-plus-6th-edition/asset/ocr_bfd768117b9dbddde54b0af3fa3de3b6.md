# Abstraction and Classes

Typically, data members go into the private section and member functions go into the public section, so a typical class declaration has this form:

```
class className
{
private:
    data member declarations
public:
    member function prototypes
};
```

The contents of the public section constitute the abstract part of the design, the public interface. Encapsulating data in the private section protects the integrity of the data and is called data hiding. Thus, using a class in the C++ way of making easy to implement the OOP features abstraction, data hiding, and encapsulation.

The second step is to implement the class member functions. You can use a complete function definition instead of a function prototype in the class declaration, but the usual practice, except with very brief functions, is to provide the function definitions separately. In that case, you need to use the scope-resolution operator to indicate which member function belongs. For example, suppose the Bozo class has a member function called Retort() that returns a pointer to a char. The function header would look like:

```
char * Bozo::Retort()
```

In other words, Retort() is not just a type char * function; it is a type char * function that belongs to the Bozo class. The full, or qualified, name of the function is Bozo::Retort(). The name Retort(), on the other hand, is an abbreviation of the qualified-name, and it can be used only in certain circonstances, such as in the code for the class methods.

Another way of describing this situation is to say that the name Retort has class scope, so the scope-resolution operator is needed to qualify the name when it is used outside the class declaration and a class method.

To create an object, which is a particular example of a class, you use the class name as if it were a type name:

Bozo bozetta.

This works because a class is a user-defined type.
You invoke a class member function, or method, by using a class object. You do so by using the dot membership operator:

```
cout << bozetta.Retort();
```

This invokes the Retort() member function, and whenever for that function refers to a particular data member, the function uses that member that has in the bozetta object.