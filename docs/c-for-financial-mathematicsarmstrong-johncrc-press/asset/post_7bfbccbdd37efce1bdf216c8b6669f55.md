
## 12.10 Summary

We have covered quite a few different topics in this chapter. Here is a brief review.

- Write getters and setters and use private data where possible.
- You can inline functions by writing the definition in the class.
- The this pointer makes writing setters easy. You can use it if you need a reference to the current instance.
- Build hierarchies of classes in order to inherit functionality.
- Use the virtual keyword to mean that a method can be overridden.
- Write =0 to mean that a function has no implementation and so create an abstract class.
- Interface classes are a special case of inheritance.
- Use forward declarations to deal with circular class declarations.
- Use static variables in classes instead of global variables. Use static functions in classes to write functions that are associated with a class in general rather than any particular instance of the class.

## Chapter 13

### The Portfolio Class

A key goal of this book is to show how to use **C++** to price a portfolio containing a variety of different options. We will achieve that goal in this chapter.

Without object orientation, this would be very difficult to achieve. But since all our option classes have a `price` function that takes a `BlackScholes-Model` as a parameter it will actually be extremely easy.

We will not introduce any new language features of **C++** in this chapter. The only new idea in this chapter will be a simple design pattern called the *factory pattern* that can be used to increase information hiding.

#### 13.1 The Priceable interface

Financially, a portfolio is just a collection of securities such as stocks, bonds, and options in various quantities. The portfolio of an investor describes their total position across all securities.

To model a portfolio in **C++** we will write a class that stores a vector of different securities and a vector of the quantities held.

We need to decide what class we will use to represent each security. This could be a stock, a bond, a derivative and so forth. The only common feature of these different securities is that they can be priced. This motivates introducing a new interface `Priceable`. Here is the interface we will use:

```cpp
class Priceable {
public:
    /* Compute the price of the security in the
       Black--Scholes world */
    virtual double price(
        const BlackScholesModel& model ) const = 0;
};
```

When writing a real financial system, the parameter passed to the `price` function would not be just a `BlackScholesModel`. In reality one would pass a more complex parameter which contains data about the entire financial market rather than data about a single stock. By using this interface for our securities, we are restricting our system to pricing securities involving only a single stock price and a fixed interest rate *r*. This will be sufficient to highlight the key ideas, but obviously would need to be revisited if one was writing a real trading system.

By making **ContinuousTimeOption** extend **Priceable**, we can ensure that all our options classes implement **Priceable**. We will leave writing additional classes **Stock** and **ZeroCouponBond** as exercises for the reader (see Exercise 13.5.1 for the definition of a zero-coupon bond).

### 13.2 The Portfolio interface and implementation

Now that we have designed our **Priceable** class it is easy to design the key functions of a **Portfolio**. A **Portfolio** class must have the following key functions:

- (i) a function to add a **Priceable** instance together with an associated quantity;
- (ii) a function to change the quantity held of a given security;
- (iii) a function **price** to compute the value of the **Portfolio**.

The last item suggests that a **Portfolio** should itself implement the interface **Priceable**. This means that it will be possible to create a **Portfolio** that itself contains **Portfolios**. This accurately reflects how banks manage their books. They organise their holdings into a number of different portfolios first by line of business, then by trading desk, then by trader. Each trader will then maintain a number of separate portfolios simply as a means of organising their work.

One can see that our **Portfolio** implementation will need some way to store objects of type **Priceable** in order to keep track of the investor’s position. It is not possible for the **Portfolio** implementation to have member variables of type **Priceable** because **Priceable** is an abstract class. For the same reason it is impossible to have a vector of **Priceable** objects. The fundamental reason for this is that member variables and elements of vectors must all be of the same size. Different **Priceable** objects will take up different amounts of memory depending upon the variables they contain.

The solution for this is for the **Portfolio** to store data using **shared_ptr**. This unavoidable use of pointers was the reason we had to introduce the topic of pointers in Chapter 11.

This leads us to the following decisions about the design for the **Portfolio** class.

- (i) Our **Portfolio** implementation will hold a vector of **shared_ptr** objects that point to **Priceable** instances.
- (ii) It will also have a vector of quantities.
- (iii) Because we need to store `shared_ptr` objects, the method to add securities will take a `shared_ptr` to a security instead of a reference to the security.

Before finalising our design we add in one further consideration. The users of the `Portfolio` class don't need to know anything about how we will choose to store the data for our `Portfolio`. Therefore it would be best to keep all this inessential detail out of the header file.

With all these considerations in mind, we can now design our `Portfolio` class.

```cpp
class Portfolio : public Priceable {
public:
    /* Virtual destructor */
    virtual ~Portfolio() {};

    /* Returns the number of items in the portfolio */
    virtual int size() const = 0;

    /* Add a new security to the portfolio, returns the index at which it was added */
    virtual int add( double quantity,
    std::shared_ptr<Priceable> security ) = 0;

    /* Update the quantity at a given index */
    virtual void setQuantity( int index,
    double quantity ) = 0;

    /* Compute the current price */
    virtual double price(
    const BlackScholesModel& model ) const = 0;

    /* Creates a Portfolio */
    static std::shared_ptr<Portfolio> newInstance();
};
```

The `Portfolio` class is an abstract class. To create a `Portfolio` a user of this class must call the *factory method* `newInstance`. This function is guaranteed to return some kind of implementation of the `Portfolio` interface, but the user does not know precisely what class will be returned. Because we don't want the user to even know the member variables of the `Portfolio` objects we return, our factory method has to return a pointer to a `Portfolio`. As usual we use `shared_ptr` to simplify memory management.

The advantage of this is that *all* implementation details are hidden in the C++ file. Information about *private* fields and methods are not given to the user. This means we can change all of these implementation details without the user even having to recompile, they just need to link to the latest library.

The implementation is all placed in the file `Portfolio.cpp`.

```cpp
class PortfolioImpl : public Portfolio {
public:
    /* Returns the number of items in the portfolio*/
    int size( ) const;
    /* Add a new security to the portfolio,
       returns the index at which it was added */
    int add( double quantity,
             shared_ptr<Priceable> security );
    /* Update the quantity at a given index */
    void setQuantity( int index, double quantity );
    /* Compute the current price */
    double price( const BlackScholesModel& model ) const;

    vector<double> quantities;
    vector< shared_ptr<Priceable> > securities;
};
```

Placing all the implementation details in the cpp file has some other advantages. Let us describe some of them now.

- (i) Our implementation class PortfolioImpl has a member variable with the rather complex type

```cpp
vector< shared_ptr< Priceable > >
```

This type is a vector of pointers to Priceable objects. It is precisely the data structure we need to store the details about the different securities that our portfolio contains. Had we declared the implementation details in a header file, the type details would be even harder to read:

```cpp
std::vector< std::shared_ptr< Priceable> >
```

This is because one should not write using namespace in a header file. Thus putting implementation details in a cpp file allows us to take fuller advantage of using namespace declarations.

- (ii) In header files, the fields of all classes will normally be declared as private to increase encapsulation. Unfortunately, this makes testing awkward. It doesn’t matter if the fields of PortfolioImpl are public. We’ve achieved perfect information hiding without the need for the private keyword.

- (iii) The header file is much less complex. Since every file that uses Portfolio needs to #include our header file, this will reduce the compilation time of classes that use Portfolio. This is a small detail for this one class, but the cumulative effect across a project can be very large. The less code you put in header files, the quicker compilation will be.
