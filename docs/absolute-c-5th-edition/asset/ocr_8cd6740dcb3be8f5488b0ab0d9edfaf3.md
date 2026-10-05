# 682 CHAPTER 15 Polymorphism and Virtual Functions

Display 15.8 Review of the Classes PFArrayD and PFArrayDBak

```
class PFArrayD {
public:
    PFArrayD( );
    -PFArrayD( );
protected:
    double *a; //for an array of doubles.
    int capacity; //for the size of the array.
    int used; //for the number of array positions currently in use.
};
```

PFArrayD::PFArrayD() : capacity(50), used(0)

```
a = new double[capacity];
```

> Some details about the base class PFArrayD. A more complete definition of PFArrayD is given in Displays 14.8 and 14.9, but this has all the details you need for this.

PFArrayD::~PFArrayD() {

```
delete [];
```

```
class PFArrayDBak : public PFArrayD {
public:
    PFArrayDBak( );
    -PFArrayDBak( );
private:
    double *b; //for a backup of main array.
    int usedB; //backup for inherited member variable used.
};
```

> The destructors should be virtual, but we had not yet covered virtual functions when we wrote these classes.

PFArrayDBak::PFArrayDBak() : PFArrayD( ), usedB(0) {

```
b = new double[capacity];
```

PFArrayDBak::~PFArrayDBak() {

```
delete b];
```

> Some details about the derived class PFArrayDBak. A complete definition of PFArrayDBak is given in Displays 14.10 and 14.11, but this display has all the details you need for this chapter.

If a class has one or more member functions that are virtual, the compiler creates what is called a virtual function table for that class. This table has a pointer (memory address) for each virtual member function. The pointer points to the location of the correct code for member function. If one virtual function was inherited and not

# virtual function table