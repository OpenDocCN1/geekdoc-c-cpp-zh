# Automatic Conversions and Type Casts for Classes 607

And even though a computer may represent an address internally with an integer, integers and pointers are conceptually quite different. For example, you wouldn't square a pointer. However, when automatic conversions fail, you may use a type cast:

```
int * p = (int *) 10; // ok, p and (int *) 10 both pointers
```

This sets the pointer to the address 10 by casting 10 to pointer-to-int (that is, type int *).Whether this assignment makes sense is another matter.

You may define a class sufficiently to a basic type or to another class that makes sense to convert from one to another automatically, perhaps, via a type cast. To see how that works, you can recast the pounds-to-stone from Chapter 3 into class form. First, you need to design an appropriate type. Fundamentally, you're representing one thing (weight) two ways (pounds and stone). A class provides an excellent way to incorporate two representations of one concept into a single entity. Therefore, it makes sense to place both representations of the weight into the same class and then provide class methods for expressing the weight in different forms. Listing 11.16 provides the class header.

```
Listing 11.16 stonew.h
// stonew.h -- definition for the Stonew class
#ifndef STONEW_H_
#define STONEW_H_
class Stonew
{
private:
    enum {Libs_per_stn = 14}; // pounds per stone
    int stone; // whole stones
    double pds_left; // fractional pounds
    double pounds; // entire weight in pounds
public:
    Stonew(double lbs); // constructor for double pounds
    Stonew(int stn, double lbs); // constructor for stone, lbs
    Stonew();
    ~Stonew(); // default constructor
    void show_lbs() const; // show weight in pounds format
    void show_stn() const; // show weight in stone format
};
#endif
```

As mentioned in Chapter 10, enum provides a convenient way to define class-specific constants, provided that they are integers. Or you could use the following alternative:

```
static const int Lbs_per_stn = 14;
```