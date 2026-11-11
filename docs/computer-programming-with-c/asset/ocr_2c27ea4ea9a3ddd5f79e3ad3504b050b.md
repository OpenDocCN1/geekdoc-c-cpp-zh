# ## 14.19 Virtual Destructors

In Chapter 11, we have mentioned that destructors can be virtual and constructors **cannot be virtual**. In this section, we will understand the usage of virtual destructors.

A non-virtual destructor does not give proper results when an object of child class is created dynamically with a parent type reference pointing to it. For example, let us consider the following piece of code in which class named Child is a child class of class named Parent. Constructor and destructor are present in both the classes Parent and Child.

```
    #include<iostream.h>
    class Parent
    {
        public:
        Parent()
        {
            cout<<"Constructor of Parent class"<<endl;
        }
        ~Parent()
        {
            cout<<"Destructor of Parent class"<<endl;
        }
    };
    class Child: public Parent
    {
        public:
        Child()
        {
            cout<<"Constructor of Child class"<<endl;
        }
        ~Child()
        {
            cout<<"Destructor of Child class"<<endl;
        }
    };
    void main()
    {
        Parent *ptr = new Child();
        delete ptr;
    }
```

The first statement in main() function

```
    Parent *ptr = new Child();
```

creates a parent type pointer named asptr. This pointer points to the object of type child. This is possible as we know that the parent type pointer can also point to any of the child objects.