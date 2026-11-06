The above syntax must be used in all cases where reference data members are used. E.g., if d_ir would have been an int reference data member, a construction like

```
Process::Process(int &ir)
:
    d_ir(ir)
{}
```

would have been required.

# ### 7.3 Data member initializers (C++11, 4.7)

Non-static data members of classes are usually initialized by the class's constructors. Frequently (but not always) the same initializations are used by different constructors, resulting in multiple points where the initializations are performed, which in turn complicates class maintenance.

Consider a class defining several data members: a pointer to data, a data member storing the number of data elements the pointer points at, a data member storing the sequence number of the object. The class also offer a basic set of constructors, as shown in the following class interface:

```
class Container
{
    Data *d_data;
    size_t d_size;
    size_t d_nr;

    static size_t s_nObjects;

    public:
        Container();
        Container(Container const &other);
        Container(Data *data, size_t size);
        Container(Container &&tmp);
};
```

The initial values of the data members are easy to describe, but somewhat hard to implement. Consider the initial situation and assume the default constructor is used: all data members should be set to 0, except for d_nr which must be given the value ++s_nObjects. Since these are non-default actions, we can't declare the default constructor using = default, but we must provide an actual implementation:

```
Container()
:
    d_data(0),
    d_size(0),
    d_nr(++s_nObjects)
{}
```

In fact, *all* constructors require us to state the d_nr(++s_nObjects) initialization. So if d_data's type would have been a (move aware) class type, we would still have to provide implementations for all of the above constructors.

The C++ standard, however, supports *data member initializers*, simplifying the initialization of non-static data members. Data member initializers allow us to assign initial values to data members. The compiler must be able to compute these initial values from initialization expressions, but the initial values do not have to be constant expressions. So ++s_nObjects can be an initial value.