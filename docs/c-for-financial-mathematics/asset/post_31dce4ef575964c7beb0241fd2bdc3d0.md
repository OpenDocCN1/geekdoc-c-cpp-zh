
## 11.5 Memory Management

The data we have used so far has all been stored in local variables or member variables.

Local variables are no good for long-term storage because their data is deleted the moment the variable goes out of scope.

Member variables only last as long as the object containing the variable. So data stored in member variables will be lost as soon as the object is deleted. Using `new`, we can create long-term storage for data. This data will not be automatically deleted, so we have to manually delete it with a call to `delete`. `new` and `delete` are just like `new[]` and `delete[]` except that they create and delete single objects rather than arrays. You have to be very careful to use `delete[]` when you have used `new []` and `delete` when you have used `new`.

Here is an example of how to create individual pair instances using `new`. Note the call to `delete` and the use of `->`.

```cpp
Pair* myPair = new Pair;
myPair->x = 1.3;
myPair->y = 2.5;

cout << "Pair (";
cout << (myPair->x);
cout << ", ";
cout << (myPair->y);
cout << ")\n";

delete myPair;
```

Let us see how to use data created in this way to share Instrument data between two positions.

First we define classes for Position and Instrument:

```cpp
class Instrument {
public:
   string bloombergTicker;
   string ricCode;
   string companyName;
   Instrument() {}
};

class Position {
public:
   string trader;
   double quantity;
   Instrument* instrument;
   explicit Position( Instrument * instrument );
};

Position::Position( Instrument* instrument ) :
    instrument( instrument ) {
}
```

You should notice that the Position contains a pointer to an Instrument and not an actual Instrument. You can see this because the type of the field `instrument` is `Instrument*`.

The code below initialises a vector of Position objects that both point to the same Instrument. This achieves our goal of sharing data.

```cpp
vector<Position> constructPositions() {
    // the caller of this function
    // should call delete on the instrument
    // when they are done with all the positions
    vector<Position> positions;

    Instrument* instrument = new Instrument;
    instrument->companyName = "Google";
    instrument->bloombergTicker = "GOOG US Equity";
    instrument->ricCode = "GOOG.OQ";

    Position p1(instrument);
    p1.trader = "Han";
    p1.quantity = 100.00;
    positions.push_back( p1 );

    Position p2(instrument);
    p2.trader = "Leia";
    p2.quantity = -100.00;
    p2.instrument = instrument;
    positions.push_back( p2 );

    return positions;
}
```

However, there is a catch, the caller of this function has been given the task of deleting the instruments.

```cpp
void testConstructPositions() {
    vector<Position> r = constructPositions();
    int n = r.size();
    for (int i=0; i<n; i++) {
        cout << "Position "<<i<<"\n";
        Position& p=r[i];
        cout << "Trader "<<p.trader<<"\n";
        cout << "Quantity "<<p.quantity<<"\n";
        cout << "Instrument ";
        cout << p.instrument->companyName<<"\n";
        cout << "\n";
    }
    delete r[0].instrument;
}
```

The caller of `constructPositions` has to know precisely how to call `delete`. This violates information hiding—you need to know how `constructPositions` actually works to be able to use it safely.

### Danger!

- **Initialise your pointers.** We have initialised the field `instrument` in the constructor. If you don’t initialise a pointer, it will fail horribly when you try to use it.

```cpp
// Don’t do this
Instrument* instrument;
cout << instrument->companyName << "\n";
```

Sometimes you wish to specify that a pointer doesn’t yet point to anything, in which case you initialise it to `nullptr`. Here is code that checks to see if a pointer is `nullptr` before using it.

```cpp
string getCompanyName( Position& position ) {
	if (position.instrument==nullptr) {
		return "Name not set";
	} else {
		return position.instrument->companyName;
	}
}
```

The danger in using `nullptr` is that if you forget the check you will get a nasty error.

## 11.6.1 Sharing with shared_ptr

The class `shared_ptr` solves the `delete` problem. To use `shared_ptr`, you need to `#include <memory>`.

`shared_ptr` is an example of a so-called “smart pointer”. This is a C++ class which behaves like a pointer but which handles working out when to call `delete` on your behalf. In fact, `shared_ptr` is the most versatile smart pointer class and the only one we will use in this book.

The way a `shared_ptr` works is that each shared pointer keeps track of how often it has been copied. Once the number of copies of the smart pointer in existence drops to zero, the data pointed to will be deleted for you. How this is actually achieved will have to wait until we discuss destructors in Section 16.2.

The changes one makes to use a **shared_ptr** are very simple. Here is a new version of the **Position** class which uses a **shared_ptr**.

```cpp
class PositionV2 {
public:
	string trader;
	double quantity;
	shared_ptr<Instrument> instrument;
	explicit PositionV2(shared_ptr<Instrument> ins );
};

PositionV2::PositionV2(shared_ptr<Instrument> ins ) :
	instrument( ins ) {
}
```

The difference is that it now contains a **shared_ptr<Instrument>** rather than an **Instrument***. The former means “shared pointer to an instrument”, the latter means “pointer to an instrument”. The former is actually easier to read, although it is undeniably harder to type.

When we use a **shared_ptr** we can use the operators **->** and **\*** just as if we were working with a pointer.

```cpp
vector<PositionV2> constructPositionsV2() {
	vector<PositionV2> positions;

	shared_ptr<Instrument> ins
		= make_shared<Instrument>();
	ins->companyName = "Google";
	ins->bloombergTicker = "GOOG US Equity";
	ins->ricCode = "GOOG.OQ";

	PositionV2 p1(ins);
	p1.trader = "Han";
	p1.quantity = 100.00;
	positions.push_back( p1 );

	PositionV2 p2(ins);
	p2.trader = "Leia";
	p2.quantity = -100.00;
	p2.instrument = ins;
	positions.push_back( p2 );

	return positions;
}
```

The key difference is that we use the function **make_shared** instead of **new** to create a **shared_ptr**.

```cpp
shared_ptr<Instrument> ins
    = make_shared<Instrument>();
```

**make_shared** is defined in `<memory>` and is part of the namespace **std**.

The payoff of introducing **shared_ptr** can be seen in the calling function.

```cpp
void testConstructPositionsV2() {
    vector<PositionV2> r = constructPositionsV2();
    int n = r.size();
    for (int i=0; i<n; i++) {
        cout << "Position "<<i<<"\n";
        PositionV2& p=r[i];
        cout << "Trader "<<p.trader<<"\n";
        cout << "Quantity "<<p.quantity<<"\n";
        cout << "Instrument ";
        cout << p.instrument->companyName<<"\n";
        cout << "\n";
    }
}
```

The essential point is that we no longer need to call **delete**, so information hiding has been restored.

### **Danger!**

Programming with raw pointers is hard. You may feel that you will never forget to call **delete**, and so you can use pointers without using **shared_ptr**, thereby writing faster code. If so, here is an example of a problem that might catch you out.

```cpp
int* a = new int [10];
int* b = new int[20000000];
cout << "Arrays created";
delete[] a;
delete[] b;
```

What's wrong with this code? Well, what happens if the second call to **new** fails because we are running short of memory and so throws an error? Then the first object will never be deleted. So your program has just leaked memory when it was already running low on memory. It will probably crash soon.

**shared_ptr** works very well for most practical purposes but it does have the problem that if you have circular references between your data objects, then they will never get deleted. The cure for this is either to avoid circular references or to use an even smarter pointer library. In this book, we choose to simply avoid circular references.

## 11.7 Sharing data with references

A lot of what you can do with a pointer, you can do with a reference. For example, you can have a member variable which is a reference. If you store data by reference you save memory just as you do if you store data by pointer.

One advantage of using references rather than pointers is that you must initialise member variables which are references in the constructor. This means that the errors you can get from null pointers and uninitialised pointers just can't happen with a reference.

However, using reference member variables is not normally as useful as choosing shared_ptr member variables. The reason is that owning a shared_ptr to an object means that you are guaranteed the object won't be deleted until you no longer need it. On the other hand, if you use a reference, there's a danger that someone else might delete your object.

Let's give an example of why you shouldn't normally use references as member variables. First we define a new Position class that contains a reference to an Instrument.

```cpp
class PositionV3 {
public:
    string trader;
    double quantity;
    Instrument& instrument;
    explicit PositionV3( Instrument& instrument );
};

PositionV3::PositionV3( Instrument& instrument ) :
    instrument(instrument) {
}
```

This code is technically correct. Notice in particular that we initialise a member variable reference in the constructor as is required.

The problem with this design is that the Position class has no control over when the instrument is deleted. The following code seems to work at first, it certainly compiles:

```cpp
PositionV3 constructPositionV3() {
    // This function doesn't work, the instrument
    // is deleted, so all the returned positions
```
