```
```
}
double getStrike() const {
return strike;
}
void setStrike(double strike) {
this->strike = strike;
}
// ... more methods ...
private:
double maturity;
double strike;
};
```
```

Notice that our base class has a virtual destructor.

```
```
virtual ~ContinuousTimeOptionBase() {}
```
```

We’ve seen these before with interface classes. Just like interface classes, any class you use as a base class must have a virtual destructor.

We can now write a class PutOption which “extends” the base class. It will automatically “inherit” all the functions.

```
```
class PutOption : public ContinuousTimeOptionBase {
public:
/* Calculate the payoff of the option given
a history of prices */
double payoff(
const std::vector<double>& stockPrices
) const;

double price( const BlackScholesModel& bsm )
const;

bool isPathDependent() const {
return false;
};
};
```
```

The first line of the code says that the class PutOption extends the class ContinuousTimeOptionBase.

```
```
class PutOption : public ContinuousTimeOptionBase {
```
```

This means that all the methods that are defined in ContinuousTimeOption-Base are automatically provided for PutOption so we don’t need to write them again.