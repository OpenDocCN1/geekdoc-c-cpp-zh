# 21 More about Inheritance 703

Suppose now that we want a pointer to the base class to point to a ProgAuth object. As we know, we can:

```
Person *p;
ProgAuth *pro_auth;
p = &pro_auth; // Compilation error.
```

However, the compiler will display an error message. Let's see why. Since each of the Programmer and Author sub-objects are derived from the Person class, the ProgAuth object also contains two Person sub-objects. Normally, as we know, when the address of a derived object is assigned to a pointer to the base class, the pointer points to the address of the base object inside the derived object. But in the ProgAuth object there are two sub-objects of the base class. Which of the two to point? Because the compiler does not know which class to choose, it displays an error similar to Person is an ambiguous base class of ProgAuth. And how can we solve this problem? We use type cast For Example:

```
Person *p1, *p2;
ProgAuth *pro_auth;
p1 = static_cast<Programmer*>(&pro_auth); /* The Person sub-object of the Programmer sub-object is selected. */
p2 = static_cast<Author*>(&pro_auth); /* The Person sub-object of the Author sub-object is selected.*
```

The last and most important question. Since a ProgAuth object has two Person sub-objects, it will have two names and two codes. What does make sense? Of course, not who is a programmer and a writer should have one name and identity like everyone, not two. And how can we make this possible? The answer is by using virtual base classes. In general, typically, we would want to avoid having multiple sub-objects, so let's see how we can do that.

# Virtual Base Classes

The declaration of a base class virtual allows an object derived from multiple classes which are derived from a common base class to contain one sub-object of that base class. In other words, to avoid a derived class to contain more than one sub-objects of the same base class, we declare that base virtual. To make the base class virtual we use the word virtual in the declaration of the derived class that inherits it. For example, in the program C.21.5 we write:

```
class B : virtual public A {......};
class C : virtual public A {......};
```

Now the B and C sub-objects share a common A sub-object. Thus, a BC object contains only one A-object. If we write:

```
bc.show_A();
```

the compiler will not display an error message, as in the case of the non-virtual A class, now the bc object contains only one A sub-object. No qualification is needed. Note that the words virtual and public can also be used in reverse order. Note also, that the same word virtual is used to denote virtual classes and virtual functions, these two concepts are different from each other. Now, why is it decided to use the same word and not introduce some new word that better demonstrates the uniqueness