# What if you omit the member initializer list?

```
RatedPlayer::RatedPlayer(unsigned int r, const string & fn,
    const string & ln, bool ht) // what if no initialization list?
{
    rating = r;
}
```

The base-class object must be created first, so if you omit calling a base-class constructor, the program uses the default base-class constructor. Therefore, the previous code is the same as the following:

```
RatedPlayer::RatedPlayer(unsigned int r, const string & fn,
    const string & ln, bool ht) // : TableTennisPlayer()
{
    rating = r;
}
```

Unless you want the default constructor to be used, you should explicitly provide the correct base-class constructor call.

Now let’s look at code for the second constructor:

```
RatedPlayer::RatedPlayer(unsigned int r, const TableTennisPlayer & tp)
    : TableTennisPlayer(tp)
{
    rating = r;
}
```

Again, the TableTennisPlayer information is passed on to a TableTennisPlayer constructor:

```
TableTennisPlayer(tp)
```

Because tp is type const TableTennisPlayer &, this call invokes the base-class copy constructor. The base class didn’t define a copy constructor, but recall from Chapter 12 that the compiler automatically generates a copy constructor if one is needed and you haven’t defined one already. In this case, the implicit copy constructor, which does memberwise copying, is fine because the class doesn’t directly use dynamic memory allocation. (The string members do use dynamic memory allocation, but, recall, memberwise copying will use the string class copy constructors to copy the string members.)

You may, if you like, also use member initializer list syntax for members of the derived class. In this case, you use the member name instead of the class name in the list. Thus, the second constructor can also be written in this manner:

```
// alternative version
RatedPlayer::RatedPlayer(unsigned int r, const TableTennisPlayer & tp)
    : TableTennisPlayer(tp), rating(r)
{
}
```