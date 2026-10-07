
However, as you've seen, a pointer to a base class can refer to a derived-class object without using an explicit type cast. For example, the following initializations are allowed:

```
BrassPlus dilly("Annie Dill", 493222, 2000);
Brass *pb = &dilly; // ok
Brass &rb = dilly; // ok
```

Converting a derived-class reference or pointer to a base-class reference or pointer is *upcasting*, and it is always allowed for public inheritance without the need for an explicit type cast. This rule is part of expressing the *is-a* relationship. A BrassPlus object is a Brass object because it inherits all the data members and member functions of a Brass object. anything that you can do with a Brass object, you can do with a BrassPlus object. A function designed to handle a Brass reference, without fear of creating problems, performs the same acts on a BrassPlus object. The same idea applies if you pass a pointer to an object as a function. Upcasting is therefore, if you define a BrassPlus class from BrassPlus, then a Brass pointer or reference can refer to a Brass object, a BrassPlus object, or a BrassPlus object.

The opposite, converting a base-class pointer or reference to a derived-class reference or pointer, is *downcasting*, and it is not allowed without an explicit type cast. The reason for this restriction is that the *is-a* relationship is not, in general, symmetric. A derived class could add new data members, and the class functions that used would not apply to the base class. For example, suppose you derive a Singer class from Employee, adding a data member representing a singer's vocal range and a member function, called range(), that reports the value for the vocal range. It wouldn't make sense to apply the range() method to an Employee object or a Singer object. But if implicit downcasting were allowed, you could accidentally set a pointer-to-Singer to the address of an Employee object and use the pointer to invoke the range() method (see Figure 13.4).

Upcasting also takes place for functions with base-class references or pointers as parameters. Consider the following code fragment, and suppose each function calls via the virtual method ViewAcct():

```
void fr(Brass &rb); // uses rb.ViewAcct()
void fp(Brass *pb); // uses pb->ViewAcct()
void fv(Brass &b); // uses b.ViewAcct()
int main {
	BrassPlus b("Betty Bee", 123432, 100000);
	BrassPlus bp("Betty Beep", 223313, 123450);
	fr(b); // uses Brass::ViewAcct()
	fp(bp); // uses BrassPlus::ViewAcct()
	fv(b); // uses Brass::ViewAcct()
	fp(bp); // uses BrassPlus::ViewAcct()
	fv(b); // uses Brass::ViewAcct()
	fv(bp); // uses Brass::ViewAcct()
}
```

Passing by value causes only the Brass component of a BrassPlus object to be passed to the fv() function. The implicit upcasting that occurs with references and pointers causes the fr() and fp() functions to use Brass::ViewAcct() for Brass objects and BrassPlus::ViewAcct() for BrassPlus objects.

Implicit upcasting makes it possible for a base-class pointer or reference to refer to either a base-class object or a derived-class object, and that produces the need for dynamic binding. Virtual member functions are the C++ answer to that need.

# Virtual Member Functions and Dynamic Binding

Let's revisit the process of invoking with a reference or pointer. Consider the following code:

```
BrassPlus ophelia; // derived-class object
Brass * bp; // base-class pointer
bp = &ophelia; // Brass pointer to BrassPlus object
bp->ViewAcct(); // which version?
```

As discussed before, if ViewAcct() is not virtual in the base class, bp->ViewAcct() goes by the pointer type (Brass *) and invokes Brass::ViewAcct(). The pointer type is known at compile time, so the compiler can bind ViewAcct() to Brass::ViewAcct() at compile time. In short, the compiler uses static binding for non-virtual methods.

But if ViewAcct() is declared virtual in the base class, bp->ViewAcct() goes by the object type (BrassPlus) and invokes BrassPlus::ViewAcct(). In this example, you can see that the object type is BrassPlus, but in general, (as in Listing 13.10) the object type generates code that binds ViewAcct() to Brass::ViewAcct() or BrassPlus::ViewAcct(), depending on the object type, while the program executes. In short, the compiler uses dynamic binding for virtual methods.

In most cases, dynamic binding is a good thing because it allows a program to choose the method designed for a particular type. Given this, you might be wondering the following:

- Why have two kinds of binding?
- If dynamic binding is so good, why isn't the default?
- How does it work?

We'll look at answers to these questions next.

# Why TwoKinds of Binding and Why Static is the Default

If dynamic binding allows you to redefine class methods but static binding makes a partial botch of it, why static binding at all? There are two reasons: efficiency and a conceptual model.

First, let's consider efficiency. For a program to be able to make a runtime decision, it has some way to keep track of what sort of object a base-class pointer or reference refers to, and that entails some extra overhead. (You'll see one method of dynamic binding later). If, for example, you design a class that won't be used as a base class for inheritance, or if you have a derived class, such as the RatedPlayer example, that does not redefine methods, then you won't need dynamic binding. Similarly, if you do, in these cases it makes sense to use static binding and gain a little efficiency. The fact that static binding is more efficient is the default choice for C++. Stroustrup says one of the principles of C++ is that you shouldn't have to pay (in memory usage or processing time) for functions that you don't use. You should go to virtual functions only if the program design needs them.

Next, consider the conceptual model. When you design a class, you may have member functions that you don't want redefined in derived classes. For example, the Balance() function, which returns the account balance, seems like a function that shouldn't be redefined. By making it nonvirtual, you accomplish two things. First, make it efficient. Second, you announce that it is your intention that this function not be redefined. That suggests reserving the virtual label just for methods you expect to be redefined.

> Tip
> If a method in a base class will be redefined in a derived class, you should not be redefined, you should make it nonvirtual.

Of course, when you design a class, it's not obvious into which category a method falls. Many aspects of real life, class design is not a linear process.

# Virtual Functions Work

C++ specifies how virtual functions should behave, but it leaves the implementation up to the compiler writer. Use virtual functions, but seeing how it is done may help you understand the concepts better, so let's take a look.

The usual way compilers handle virtual functions is to add a hidden member to each object. The hidden member holds a pointer to an array of addresses. Such an array is termed a virtual function table (vtable). The vtable holds the addresses of the virtual functions declared for objects of that class. For example, an object of a base class contains a pointer to a table of addresses of all the virtual functions for that. An object of a derived class contains a pointer to a separate table of addresses. If the derived class provides a new definition of a virtual function, the vtable holds the address of the new function.

# Static and Dynamic Binding

If the derived class does not redefine the virtual function, the vtable holds the address of the original version. If the derived class defines a new function and makes it virtual, its address is added to the vtable (see Figure 13.5). Note that whatever you define 1 or 10 virtual functions for a class, you add just one address to an object; it's the size that varies.

```
class Scientist{
    char name[40];
    public:
        virtual void show_name();
        virtual void show_all();
    };
    class Physicist : public Scientist {
        char field[40];
        public:
            void show_all(); // redefined
            virtual void show_field(); // new (function)
    };
```

address of address of Scientist::show_name() Physicist::show_all()

Scientist virtual function table

| | 4064 | 6400 |
|---|---|---|
| | 6820 | 7280 |

Physicist virtual function table

address address of Scientist::show_name() Physicist::show_all() Physicist::show_field() (function not redefined)

Scientist object with hidden pointer member vptr, which points to Scientist virtual function table

| Sophie Fant | 2008 |
|---|---|
| name | vptr |
| Adam Crusher | 2096 | nuclear structure |
| name | vptr | field |

Physicist with hidden pointer member vptr, which points to Physicist virtual function table

Physicist adam("Adam Crusher", "nuclear structure"); Scientist * psc = &adam; psc->show_all();

+   1. Find value of psc->vptr, which is 2096.
2. Go to address at 2096.
3. Find address of second function in table, which is 6820.
4. Go to address (6820) and execute the function there.

Figure 13.5 A virtual function mechanism.
