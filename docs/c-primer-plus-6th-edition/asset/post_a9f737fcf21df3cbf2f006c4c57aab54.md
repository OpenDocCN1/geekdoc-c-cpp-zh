
```cpp
cout << "Trying to get a big block of memory:\n";
pb = new Big[10000]; // 1,600,000,000 bytes
cout << "Got past the new request:\n";
}
catch (bad_alloc& ba)
{
    cout << "Caught the exception!\n";
    cout << ba.what() << endl;
    exit(EXIT_FAILURE);
}
cout << "Memory successfully allocated:\n";
pb[0].stuff[0] = 4;
cout << pb[0].stuff[0] << endl;
delete [] pb;
```

Here's the output for the system:
Trying to get a big block of memory:
Caught the exception!
std::bad_alloc

In this case, the what () method returns the string "std::bad_alloc".
If the program runs without allocation problems on your system, you can try increasing the amount of memory requested.

## The Null Pointer and new

Much code was written when new (the old new) returned a null pointer upon failure. Some compilers handled the transition to the new new by letting the user set a flag or switch to choose which behavior stayed. Currently, the standard provides for an alternative form of new that still returns a null pointer. Its use looks like this:

```cpp
int * pi = new (std::nothrow) int;
int * pa = new (std::nothrow) int[500];
```

Using this function, you could rewrite the core of Listing 15.13 this way:
Big * pb;

```cpp
pb = new (std::nothrow) Big[10000]; // 1,600,000,000 bytes
if (pb == 0)
{
    cout << "Could not allocate memory. Bye.\n";
    exit(EXIT_FAILURE);
}
```

## Exceptions, Classes, and Inheritance

Exceptions, classes, and inheritance interact in a couple ways. First, you can derive one exception class from another, as the standard C++ library does. Second, you can incorpore exceptions into classes by nesting exception declarations inside a class definition. Third, such nested declarations can be inherited and serve as base classes themselves.

Listing 15.14 starts us on the way to exploring some of these possibilities. This header file declares a rudimentary Sales class that holds a value and an array of 12 monthly sales figures. The LabeledSales class derives from Sales and adds a member to hold a label for the data.

## Listing 15.14 sales.h

```cpp
//sales.h
// exceptions and inheritance
#include <stdexcept>
#include <string>

class Sales
public:
    enum {MONTHS = 12}; // could be a static const
    class bad_index : public std::logic_error
    private:
        int bi; // bad index value
    public:
        explicit bad_index(int ix,
            const std::string & s = "Index error in Sales object\n");
        int bi_val() const throw { return bi; }
        virtual ~bad_index() throw() {}
    };
    explicit Sales(int yy = 0);
    Sales(int yy, const double * gr, int n);
    virtual ~Sales() throw() {}
    int Year() const { return year; }
    virtual double operator[](int i) const;
    virtual double &operator[](int i);
    private:
        double gross[MONTHS];
        int year;
};

class LabeledSales : public Sales
{
public:
    class nbad_index : public Sales::bad_index
    {
private:
        std::string lbl;
public:
        bad_index(const std::string& lb, int ix,
            const std::string& s = "Index error in LabeledSales object\n");
        const std::string& label_val() const { return lbl; }
        virtual ~nbad_index() throw() {};
        explicit LabeledSales(const std::string& lb = "none", int yy = 0);
        LabeledSales(const std::string& lb, int yy, const double * gr, int n);
        virtual ~LabeledSales() {}
        const std::string& Label() const { return label; }
        virtual double operator[](int i) const;
        virtual double& operator[](int i);
    private:
        std::string label;
    };
```

Let's examine a few details of Listing 15.14. First, the symbolic constant is in the protected section of Sales; this makes the value available to derived classes, such as LabeledSales. The next, bad_index class is nested in the public section of LabeledSales, which makes the class available as a type to catch blocks. Note that the outside world requires the type to be identified as Sales::bad_index. This class derives from the standard logic_error class. The bad_index class has the ability to store and report an out-of-bounds value for array index. The nbad_index class is nested in the public section of LabeledSales, making it available to client code. Because bad_index derives from logic_error, nbad_index also ultimately derives from logic_error. Both classes have overloaded operator[] methods designed to access individual elements and to throw an exception if an index is out of bounds. The reason is that both inherently inherit from the exception class, and its virtual destructor uses the throw() specification. This is a C++98 feature; under C++11 the exception doesn't have an exception specification. Listing 15.15 shows the implementation of the methods that weren't already defined inline in Listing 15.14. Note that nested classes require scope-resolution operator more than once.

## Listing 15.15 sales.cpp

```cpp
// sales.cpp -- Sales implementation
#include "sales.h"
using std::string;

Sales::bad_index(int ix, const string & s)
    : std::logic_error(s), bi(ix) {}

Sales::Sales(int yy) : year(yy) {
    for (int i = 0; i < MONTHS; ++i)
        gross[i] = 0;

Sales::Sales(int yy, const double * gr, int n) : year(yy) {
    int lim = (n < MONTHS) ? n : MONTHS;
    int i;
    for (i = 0; i < lim; ++i)
        gross[i] = gr[i];
    for (i = lim; i < MONTHS; ++i)
        gross[i] = 0;

double Sales::operator[](int i) const {
    if (i < 0 || i >= MONTHS)
        throw bad_index(i);
    return gross[i];
}

double& Sales::operator[](int i) {
    if (i < 0 || i >= MONTHS)
        throw bad_index(i);
    return gross[i];
}

LabeledSales::nbad_index(const string& lb, int ix, const string& s)
    : Sales::bad_index(ix, s), lbl(lb) {}

LabeledSales::LabeledSales(const string& lb, int yy)
    : Sales(yy), label(lb) {}

LabeledSales::LabeledSales(const string& lb, int yy, const double * gr, int n)
    : Sales(yy, gr, n), label(lb) {}

double LabeledSales::operator[](int i) const {
    if (i < 0 || i >= MONTHS)
        throw nbad_index(label, i);
    return Sales::operator[](i);
}

double& LabeledSales::operator[](int i) {
    if (i < 0 || i >= MONTHS)
        throw nbad_index(label, i);
    return Sales::operator[](i);
}
```

## Listing 15.16 use_sales.cpp

```cpp
// use_sales.cpp -- nested exceptions
#include <iostream>
#include "sales.h"

int main()
{
  using std::cout;
  using std::cin;
  using std::endl;

  double vals1[12] =
    {
        1220, 1100, 1122, 2212, 1232, 2334,
        2884, 2393, 3302, 2922, 3002, 3544
    };

  double vals2[12] =
    {
        12, 11, 22, 21, 32, 34,
        28, 29, 33, 29, 32, 35
    };

  Sales sales1(2011, vals1, 12);
  LabeledSales sales2("Blogstar", vals2, 12);

  cout << "First try block:\n";
  try{
    int i;
    cout << "Year = " << sales1.Year() << endl;
    for (i = 0; i < 12; ++i)
    {
        cout << sales1[i] << ' ' ';
        if (i % 6 == 5)
            cout << endl;
    }
    cout << "Year = * " << sales2.Year() << endl;
    cout << "Label = " << sales2.Label() << endl;
    for (i = 0; i < 12; ++i)
        {
            cout << sales2[i] << ' ' ';
            if (i % 6 == 5)
                cout << endl;
        }
    cout << "End of try block 1.\n";
  } catch (LabeledSales::nbad_index & bad)
  {
    cout << "Company: " << bad.label_val() << endl;
    cout << "bad index: " << bad.bi_val() << endl;
  }
  catch(Sales::bad_index & bad)
  {
    cout << bad.what();
  }

  cout << "\nSecond try block:\n";
  try{
    int i;
    cout << "Year = " << sales1.Year() << endl;
    for (i = 0; i < 12; ++i)
    {
        cout << sales1[i] << ' ' ';
        if (i % 6 == 5)
            cout << endl;
    }
    cout << "Year = * " << sales2.Year() << endl;
    cout << "Label = " << sales2.Label() << endl;
    for (i = 0; i < 12; ++i)
        {
            cout << sales2[i] << ' ' ';
            if (i % 6 == 5)
                cout << endl;
        }
    cout << "End of try block 2.\n";
  } catch (LabeledSales::nbad_index & bad)
  {
    cout << "Company: " << bad.label_val() << endl;
    cout << "bad index: " << bad.bi_val() << endl;
  }
  catch(Sales::bad_index & bad)
  {
    cout << bad.what();
  }

  return 0;
}
```
