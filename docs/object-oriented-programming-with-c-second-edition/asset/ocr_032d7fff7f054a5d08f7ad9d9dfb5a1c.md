# Classes and Objects

```
class A
```

```
{
public:
    friend void B::test_friend(const int=0);
```

```
};
```

```
inline void B::test_friend(const int p)
{
    APtr->x=p;
}
/*End of friendMemInline.h*/
```

# Friends as bridges

Friend functions can be used as bridges between two classes.
Suppose there are two unrelated classes whose private data members need a simultaneous update through a common function. This function should be declared as a friend to both the classes. See Listing 2.29.

Listing 2.29 Friends as bridges

```
class B; //forward declaration
class A
{
    /*
    rest of the class A
    */
    friend void ab(const A&, const B&);
};
class B
{
    /*
    rest of the class B
    */
    friend void ab(const A&, const B&);
};
```

# 2.2.7 Static Members

# Static member data

Static members hold global data that is common to all objects of the class. Examples of such global data are

+   - count of objects currently present,
- common data accessed by all objects, etc.

Let us consider Account. We want all objects of this class to calculate interest at the rate of 4.5%. Therefore, this data should be globally available to all objects of this class (Listing 2.30).

This data cannot should be a member of the objects themselves. Otherwise, multiple copies of this data will be embedded within the objects taking up unnecessary space.