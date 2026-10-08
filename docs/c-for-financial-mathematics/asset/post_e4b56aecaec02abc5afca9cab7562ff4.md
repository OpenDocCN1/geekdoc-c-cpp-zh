
## 10.5 What's wrong with if statements?

A useful mental picture is to think of an object as some data and an instruction manual explaining how to make sense of the data.

When we want to price an option we need to know the strike, the maturity, and also some instructions on how to compute the payoff at maturity. These instructions take the form of a function called **payoff**.

When we call the **price** function on our **MonteCarloPricer** we pass an option object as the first parameter. This object contains all the data we need plus all the instructions we need. When given an option to price, the **price** function looks up the **getMaturity** and the **payoff** functions in the index of the instruction manual, and uses these instructions to perform the computation. Implementing an interface is simply a way of stating clearly that the **getMaturity** and **payoff** functions will be there when needed.

This simple metaphor is the heart of object-oriented programming. When writing software you should pass round not just data, but also the instruction manual for working with that data. An object is nothing but some data and an instruction manual. This is why we pass objects as parameters. This is why we write object-oriented programs.

There are many object-oriented programming languages other than C++. Some other examples that are popular in the financial industry are Java and C#. Object-oriented programming principles are the same in different languages. For this reason a simple system of pictures was invented which allows you to draw the essential features of your software design without worrying about language-specific details. This system of pictures is called UML (Unified Modelling Language). Figure 10.1 shows the UML diagram for our **CallOption**, **PutOption**, and **PathIndependentOption** classes.

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_189_0.png)

**FIGURE 10.1**: UML diagram for **PathIndependentOption**

The dotted arrows in Figure 10.1 tell us that the **CallOption** and the **PutOption** classes implement the interface. The *italics* tell us that **PathIndependentOption** is an interface and that the methods are only declared by **PathIndependentOption** but not defined.

The advantage of the UML diagram is that it strips away some of the more ugly C++ syntax such as the **virtual destructor** and the **virtual** keyword and lets you see the main points. These main points are:

- All **PathIndependentOption** objects must have a **getMaturity** and a **payoff** function.
- **CallOption** and **PutOption** are two kinds of **PathIndependentOption**.

The UML specification provides an official standard for drawing class diagrams. For example, the + signs are used to indicate that methods are public. Don't be too pedantic about this kind of minor detail when you draw diagrams of your classes. The aim is to produce diagrams that help you summarise what is going on. Just use the parts of UML that you find helpful.

It may have struck you that there is an alternative to using interfaces. Couldn't we write a class such as the class **GeneralOption** given below?

```cpp
class GeneralOption {
public:
    bool isPut;
    bool isDigital;
    double strike;
    double maturity;

    double payoff( double stockPrice );
};
```

You are correct. The payoff function would be a little complex but wouldn't be too difficult to write. This would solve the problem of writing one function that prices puts, calls, digital puts, and digital calls.

However, the real benefit of using interfaces is that our **MonteCarloPricer** can already price any path-independent option. It isn't restricted to digital puts and calls. We will be able to use our **MonteCarloPricer** to price options you've never thought of before: For example, an option whose payoff is given by the tenth root of the stock price.

Even more interesting, observe that the **MonteCarloPricer** code and all the existing option classes will remain completely unchanged even when you think of a new option you want to price. This makes the **MonteCarloPricer** pluggable. You can extend its functionality by simply plugging in new options. It is interesting to note once again that electrical plugs are "pluggable" precisely because they have a well-defined interface.

In the context of writing financial software, the use of interfaces means you can extend a trading system with new types of financial contracts, without having to rewrite and test the whole trading system. Interfaces are the key to solving the complexity issues of writing real financial software.

## 10.6 An interface for integration

The difficulty with interfaces is not in the syntax or in the concept itself, but in spotting when you can use an interface to solve a problem. For example, we can use interfaces to perform numerical integration, but perhaps the connection between integration and interfaces is not obvious.

If you attempt to write numerical integration code in C++ you will hit a very similar problem to the one we experienced with our Monte Carlo pricer. For example, you should find it easy to write a function that integrates $e^{-x^2}$ from $a$ to $b$ using the rectangle rule. But how could you write a function that can integrate any real valued function from $a$ to $b$ using the rectangle rule? Interfaces solve this problem.

Let us proceed in the same way as the last example by writing our fantasy code. Here it is:

```cpp
double integral( RealFunction& f, double a, double b, int nPoints ) {
    double h = (b-a)/nPoints;
    double x = a + 0.5*h;
    double total = 0.0;
    for (int i=0; i<nPoints; i++) {
        double y = f.evaluate(x);
        total+=y;
        x+=h;
    }
    return h*total;
}
```

Our fantasy code involves a type called **RealFunction**. This name describes the kinds of object we can integrate. We need to write the formal C++ interface definition.

```cpp
class RealFunction {
public:
    /* A virtual destructor */
    virtual ~RealFunction() {};
    /* This method is abstract, there is no definition */
    virtual double evaluate( double x ) = 0;
};
```

This code contains the necessary **virtual** and **=0** magical incantations, but more importantly it states that a **RealFunction** has an **evaluate** method.

Our **integrate** function can integrate any object that provides an **evaluate** method. Here is an example of a specific implementation of our fantasy interface:

```cpp
class SinFunction : public RealFunction {
   double evaluate( double x );
};

double SinFunction::evaluate( double x ) {
   return sin(x);
}
```

The class **SinFunction** represents the mathematical sin function through its **evaluate** method. We can integrate it using our **integrate** function because our **integrate** function uses nothing other than the **evaluate** method.

Combining our **integrate** function, the **RealFunction** interface and its implementation, we can now write the code to integrate sin. Here is a test that everything fits together:

```cpp
static void testIntegral() {
   SinFunction integrand;
   double actual = integral(integrand, 1, 3, 1000 );
   double expected = -cos(3.0)+cos(1.0);
   ASSERT_APPROX_EQUAL( actual, expected, 0.000001);
}
```

This code is included in **FMLib10**. You should check that you can compile and run the test.

Every time we want to integrate a real valued function, we will need to write a new implementation class like **SinFunction**. We don't want to create a new **cpp** file and a new **h** file every time we want to integrate a function, so C++ gives us a shorthand notation that allows us to define a class inside a function. Here is an alternative way of testing the integral of sin using a *local class*.

```cpp
static void testIntegralVersion2() {
   class Sin : public RealFunction {
   public:
      double evaluate( double x ) {
         return sin(x);
        }
    };

        Sin integrand;
        double actual = integral(integrand, 1, 3, 1000 );
        double expected = -cos(3.0)+cos(1.0);
        ASSERT_APPROX_EQUAL(actual, expected, 0.000001);
}
```

Local classes defined in this way are “throwaway”. They can only be used inside that one function. The advantage of local classes is that the class is quicker to write. Notice that in the local class declaration we actually provide the definition for all the functions as well as the declaration. Note also that this definition doesn’t contain the usual **SinFunction::** qualification you need for a standalone class.

Here is a more elaborate example where the local class uses a member variable to access the parameters passed into the containing function.

```cpp
static double integratePayoff(
    double a,
    double b,
    const PathIndependentOption& option) {

    class PayoffFunction : public RealFunction {
    public:
        /*  Member variable */
        const PathIndependentOption& option;

        /*  Constructor */
        PayoffFunction(
            const PathIndependentOption& option)
        : option( option ) {
        }

        /**
         *  Overriding function
         */
        double evaluate(double x) {
            return option.payoff(x);
        }
    };

    PayoffFunction integrand(option);
    return integral (integrand, a, b, 1000);
}
```
