# CHAPTER 14 Inheritance

# EXAMPLE: (continued)

```
delete [] b;
```

The memory for the inherited array is also sent back to the frestore, even though you do not see any mention of a in a destructor for the derived class PFArrayDBak. When the destructor for the derived class PFArrayDBak is invoked, it ends its action by automatically invoking the destructor for the base class PFArrayD; that includes the following code to dispose of a:

```
delete [] a;
```

A demonstration program for our class PFArrayDBak is given in Display 14.12.

Figure 14.8 Interface for the Base Class PFArrayD (part 1 of 2)

```
//This is the header file pfarrayd.h. This is the interface for the
//class PFArrayD. Objects of this type are partially filled arrays
//of doubles.
#ifndef PFARRAYD_H
#define PFARRAYD_H
nclass PFArrayD
{
public:
    PFArrayD();
    //Initializes with a capacity of 50.
    PFArrayD(int capacity);

    PFArrayD(const PFArrayD& pfaObject);

    void addElement(double element);
    //Precondition: The array is not full.
    //Postcondition: The element has been added.

    bool full() const;
    //Returns true if the array is full, false otherwise.

    int getCapacity() const;
    void emptyArray();
    //Resets the number used to zero, effectively emptying the array.

    double& operator[](int index);
    //Read and change access to elements 0 through numberUsed - 1.
```