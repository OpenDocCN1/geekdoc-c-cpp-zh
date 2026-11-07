Before looking at details of Listing 13.8, such as handling of formatting in some of the methods, let’s examine the aspects that relate directly to inheritance. Keep in mind that the derived class does not have direct access to private base-class data; the derived class has to use base-class public methods to access that data. The means of access depends on the method. Constructors use one technique, and other member functions use a different technique.

The technique that derived-class constructors use to initialize base-class private data is the member initializer list syntax. The RatedPlayer class constructors use that technique, and so do the BrassPlus constructors:

```
```cpp
BrassPlus::BrassPlus(const string & s, long an, double bal,
                     double ml, double r) : Brass(s, an, bal)
{
    maxLoan = ml;
    owesBank = 0.0;
    rate = r;
}
```
```

```
```cpp
BrassPlus::BrassPlus(const Brass & ba, double ml, double r)
                 : Brass(ba)   // uses implicit copy constructor
{
    maxLoan = ml;
    owesBank = 0.0;
    rate = r;
}
```
```

Each of these constructors uses the member initializer list syntax to pass base-class information to a base-class constructor and then uses the constructor body to initialize the new data items added by the BrassPlus class.

Non-constructors can’t use the member initializer list syntax. But a derived-class method can call a public base-class method. For instance, ignoring the formatting aspect, the core of the BrassPlus version of ViewAcct() is this:

```
```cpp
// redefine how ViewAcct() works
void BrassPlus::ViewAcct() const
{
...
    Brass::ViewAcct();   // display base portion
    cout << "Maximum loan: $" << maxLoan << endl;
    cout << "Owed to bank: $" << owesBank << endl;
    cout << "Loan Rate: " << 100 * rate << "%\n";
...
}
```
```

In other words, BrassPlus::ViewAcct() displays the added BrassPlus data members and calls on the base-class method Brass::ViewAcct() to display the base-class data members. Using the scope-resolution operator in a derived-class method to invoke a base-class method is a standard technique.