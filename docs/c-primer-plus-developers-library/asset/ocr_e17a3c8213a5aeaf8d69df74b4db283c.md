```
void inadequate(Brass ba)
{
    ba.ViewAcct();
    cout << endl;
}
```

The first function passes an object by reference, and the second passes an object by value. Now suppose you use each with a derived class argument:

```
BrassPlus buzz("Buzz Parsec", 00001111, 4300);
show(buzz);
inadequate(buzz);
```

The show() function call results in the rba argument being a reference to the BrassPlus object buzz, so rba.ViewAcct() is interpreted as the BrassPlus version, as it should be. But in the inadequate() function, which passes an object by value, ba is a Brass object constructed by the Brass (const Brass &) constructor. (Automatic upcasting allows the constructor argument to refer to a BrassPlus object.) Thus, in inadequate(), ba.ViewAcct() is the Brass version, so only the Brass component of buzz is displayed.

# Destructor Considerations

As mentioned earlier, a base class destructor should be virtual. That way, when you delete a derived object via a base-class pointer or reference to the object, the program uses the derived-class destructor followed by the base-class destructor rather than using only the base-class destructor.

# Friend Considerations

Because a friend function is not actually a class member, it’s not inherited. However, you might still want a friend function to a derived class to use a friend to the base class. The way to accomplish this is to type cast a derived-class reference or pointer to the base-class equivalent and to then use the type cast reference or pointer to invoke the base-class friend:

```
ostream & operator<<(ostream & os, const hasDMA & hs)
{
    // type cast to match operator<<(ostream & , const baseDMA &)
    os << (const baseDMA &) hs;
    os << "Style: " << hs.style << endl;
    return os;
}
```

You can also use the dynamic_cast<> operator, discussed in Chapter 15, “Friends, Exceptions, and More,” for the type cast:

```
os << dynamic_cast<const baseDMA &> (hs);
```

For reasons discussed in Chapter 15, this would be the preferred form of type cast.