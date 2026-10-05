# 452 CHAPTER 10 Pointers and Dynamic Arrays

```
for (int i = 0; i < length; i++)
    a[i] = rtSide.a[i];

return *this;
}
```

A complete example with an overloaded assignment operator is given in the next programming example.

# Display 10.10 Definition of a Class with a Dynamic Array Member

```
//Objects of this class are partially filled arrays of doubles.
class PFArrayD {
public:
    PFArrayD( );
    //Initializes with capacity of 50.
    PFArrayD(int capacityValue);
    PFArrayD(const PFArrayD& pfaObject);
    void addElement(double element);
    //Precondition: The array is not full.
    //Postcondition: The element has been added.
    bool full() const { return (capacity == used); }
    //Returns true if the array is full, false otherwise.
    int getCapacity() const { return capacity; }
    int getNumberUsed() const { return used; }
    void emptyArray(int used = 0; //Empties the array.
    double& operator(int index);
    //Read and access change to elements 0 through numberUsed
    PFArrayD& operator =(const PFArrayD& rightSide);
private:
    PFArrayD( );
    double *a;//For an array of doubles
    int capacity; //For the size of the array
    int used; //For the number of array positions currently in use
};
```