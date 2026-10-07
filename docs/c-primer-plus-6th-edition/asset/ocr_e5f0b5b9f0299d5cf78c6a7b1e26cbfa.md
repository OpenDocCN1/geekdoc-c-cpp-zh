# Constructors: Access Considerations

A derived class does not have direct access to the private members of the base class; it has to work through the base-class methods. For example, the RatedPlayer constructors can not directly set the inherited members (firstname, lastname, and hasTable). Instead, they have to use public base-class methods to access private base-class members. In particular, the derived-class constructors have to use the base-class constructors.

When a program constructs a derived-class object, it first constructs the base-class object. Conceptually, that means the base-class object should be constructed before the program enters the body of the derived-class constructor. C++ uses the member initializer syntax to accomplish this. For instance, here is the code for the first RatedPlayer

```
RatedPlayer::RatedPlayer(unsigned int r, const string & fn,
    const string & ln, bool ht) : TableTennisPlayer(fn, ln, ht)
{
    rating = r;
}
```

The following part is the member initializer list:

: TableTennisPlayer(fn, ln, ht)

It is executable, and it calls the TableTennisPlayer constructor. Suppose, for example, a program has the following declaration:

RatedPlayer rplayer1("Mallory", "Duck");

The RatedPlayer constructor assigns the actual arguments "Mallory", "Duck", and true to the formal parameters fn, ln, and ht. It then passes these parameters as actual arguments to the TableTennisPlayer constructor. This constructor, in turn, creates the embedded TableTennisPlayer object and stores the data "Mallory", "Duck", and true in it. Then the program enters the body of the RatedPlayer constructor, completes the construction of the RatedPlayer object, and assigns the value of the parameter r (that is, 1140) to the rating member (see Figure 13.2 for another example).

| derived-class constructor | base-class constructor |
|---|---|
| Overdraft::Overdraft | passing arguments from the derived-class constructor to the base-class constructor

```
Overdraft::Overdraft(const char * s, long an, double bal)
{
    double ml, double r) : BandAccount(s, an, bal)
...
}
```

Figure 13.2 Passing arguments through a base-class constructor.