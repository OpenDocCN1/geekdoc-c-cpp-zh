# ## 12.2   The this keyword

In order to hide information, it is a good idea to have no **public** variables. We have just seen how to write a **get** method to provide read access to a variable. In the example below we show how to write a **set** method to provide write access.

```
```cpp
class Point {
public:
  double getX() const {
      return x;
  }
  void setX(double x) {
      this->x = x;
  }
  // other members of Point
private:
  double x;
  double y;
};
```
```

We have used the new keyword **this**. When implementing a member function the variable **this** always contains a pointer to the current object. So you can use **this->** to access the fields of the current object. We’ve just demonstrated this with the **set** method.

You can also use ***this*** to obtain a reference to the current object. To see why you might want to do this, suppose that we want to add a *price* method to a class **UpAndOutOption**. We decide that to implement this, we’ll simply pass the necessary data to our existing **MonteCarloPricer** class and ask it to perform the calculation. However, the class **MonteCarloPricer** requires you to pass it an option object. Where do we find a reference to the appropriate option object? ***this*** is just what we need to pass to the pricer.

```
```cpp
double UpAndOutOption::price(
    const BlackScholesModel& model ) const {
  MonteCarloPricer pricer;
  return pricer.price( *this, model );
}
```
```