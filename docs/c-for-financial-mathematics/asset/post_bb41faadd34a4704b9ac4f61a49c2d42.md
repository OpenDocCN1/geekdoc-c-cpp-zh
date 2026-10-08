
bool isPathDependent() const {
    return false;
};
};

The implementation of **PathIndependentOption** does the following.

- It provides an implementation of `isPathDependent`.
- It has an abstract function to compute the payoff given only the final stock price. By definition of “path independent” a path-independent option should be able to provide an implementation of this function.
- This means we can implement the `payoff` function that takes an entire path of stock prices. We only need to look at the last price.

Once we’ve written a **PathIndependentOption** class, we can use this to write a **CallOption** class that extends it.

class CallOption : public PathIndependentOption {
public:

    double payoff( double stockAtMaturity ) const;

    double price( const BlackScholesModel& bsm )
        const;
};

To implement a **CallOption** we will have to write a function to compute the payoff at maturity. So the `payoff` function above must be declared.

We have also chosen to provide an override for `price`. This is because we know that it would be better to use the Black–Scholes formula to price a Call Option than to use the default Monte Carlo implementation.

Notice that all the functions `getMaturity`, `getStrike`, etc., are implemented by the grandparent **ContinuousTimeOptionBase**.

Similarly, the **ContinuousTimeOption** method `payoff` is implemented by the parent **PathIndependentOption**, so we only have to implement a simpler method that computes the payoff using the price at maturity.

We could write **PutOption**, **DigitalCallOption**, and **DigitalPutOption** in a similar way with very little additional code. This is left as an exercise.

## 12.6.1 UML

Figure 12.1 shows a UML diagram for the class hierarchy of options in FMLlib12. Actually, the **DigitalPutOption** and **DigitalCallOption** don’t exist. You should write them yourself as an exercise.

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_236_0.png)

mean “extends”. The boxes denote classes. UML uses other types of arrows to indicate other relationships between classes. We will see examples later. We have followed the standard practice in UML of using *italics* to indicate abstract classes and roman type to indicate concrete classes.

This UML diagram is unusually complex. Class hierarchies are usually much simpler. We have tried to simplify the diagram a little by omitting all details about the member functions and variables of our classes.

Our complex hierarchy is justified because it represents the “true” relationship between options. `CallOptions` really are `PathIndependentOptions` which really are `ContinuousTimeOptions`. This is a pattern you should follow in general. You should only use subclassing to mean “is a”. All the arrows in our UML diagram can be read as “is a”.

# What good software looks like

Which artist do you prefer, Mark Rothko or Hieronymus Bosch? If you are not familiar with their paintings, they are both great painters and are polar opposites in their style. Rothko is known for abstract paintings which have a stunning simplicity. Bosch is known for his detailed landscapes of fantastic imagery.

When it comes to art, you don’t actually have to pick a favourite. But in software design you should always prefer the simplest solution to a problem.

This means that when you design your classes you should aim for a UML diagram that looks more like a Rothko than a Bosch.

## 12.6.2 Another object hierarchy

To give another example hierarchy, the **geometry** library has been updated to contain an interesting object hierarchy. It contains the following.

- A class **Shape** that represents any finite shape in the plane. It has the following methods.
    - A method **area** to compute the area.
    - A method **contains** to test if a point is in the shape.
    - A method **boundingRectangle** that returns a **Rectangle** containing the entire shape.
- The class **Circle** is one implementation of **Shape**.
- The class **Rectangle** is another implementation of **Shape**.
- The class **HyperCircle** (the shape $x^4+y^4<1$) is another implementation of **Shape**.
- The class **Shape** has a default implementation for **area** that uses Monte Carlo.
- **Circle** and **Rectangle** override **area**.

These classes would be useful in a graphics library.

Notice the importance of abstract functions and overriding. No one would want a graphics library whose **Shape** class couldn't be extended. Similarly no one would want a pricing library where you couldn't define new types of options.

These examples strike at the heart of object-oriented programming. Abstract methods and overriding methods allow you to write “pluggable” systems.

## 12.6.3 Multiple inheritance

In C++ a class can extend more than one base class. This is called *multiple inheritance*.

Multiple inheritance is useful to indicate that a class implements more than one interface.

As an example, it might be useful to have an interface **DerivativeWithStrike** for derivatives that have some associated strike price such as call options and put options (but not futures). The interface would simply return the strike price as shown below:

class DerivativeWithStrike {
public:
    ~DerivativeWithStrike();
    virtual double getStrike() const = 0;
};

To declare that a ContinuousTimeOptionBase implements both ContinuousTimeOption and DerivativeWithStrike, one would write:

class ContinuousTimeOptionBase :
    public ContinuousTimeOption,
    public DerivativeWithStrike {
};

When using multiple inheritance, I recommend that you ensure that at most one of the parent classes is a non-interface class. This is not a rule that is enforced by C++, but if you break it you will have to understand the detailed rules of multiple inheritance in C++. This makes your code harder to understand and therefore harder to maintain.

**Tip: Multiple inheritance**
Only use multiple inheritance to show that a class implements more than one interface.

We have only shown how to publicly extend from another class. This is why we use the keyword public whenever we extend a class. It is also possible to extend a class privately, but this is not a very useful feature. I recommend you do not use it.

**Danger!**
C++ is a difficult language with many advanced features. Other object-oriented programming languages such as Java do not allow multiple inheritance (except of interfaces) and do not have a concept of private inheritance. This provides evidence that these features of C++ are not widely seen to be particularly beneficial. They are best avoided.

## 12.6.4 Calling superclass methods

Sometimes it is useful to be able to call a superclass's methods. For example, consider an UpAndOutOption. If the barrier is lower than the current price, the option is worthless and so it shouldn't be priced by a slow Monte Carlo method. However, the rest of the time, one would want to use the default behaviour of the parent class, KnockoutOption, which is to price the option by Monte Carlo.

The code required to do this is as follows:

double price(
    const BlackScholesModel& model) const {
    if (model.stockPrice >= getBarrier())
        return 0;
    return KnockoutOption::price(model);
}

The key line is the last one, where we qualify the call to the function price with the name of the superclass KnockoutOption. If we didn't specify that we wanted to call the superclass's price function, the function would recursively call itself. The program would then crash with a stack overflow error.

## 12.7 Forward declarations and the structure of cpp files

The class Shape has a method boundingRectangle. This method returns a Rectangle. This means it is impossible to write the class Shape without first having told the compiler about the class Rectangle.

On the other hand, a Rectangle is a Shape itself, so we have a circularity. This seems to make it impossible to declare either Rectangle or Shape.

To deal with the problem you can use a forward declaration of the class Rectangle. Here's an example of how to make forward declarations:

class CartesianPoint;
class Rectangle;

class Shape {
public:
    /* Does the point lie in the shape */
    virtual bool contains(const CartesianPoint& point)
        const = 0;
    /* A rectangle bounding the shape */
    virtual Rectangle boundingRectangle() const = 0;
    /* By default area is computed by Monte Carlo */
    virtual double area() const;
};

The forward declarations:

class CartesianPoint;
