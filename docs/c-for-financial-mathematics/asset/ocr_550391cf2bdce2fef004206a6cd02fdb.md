```
class BlackScholesModel {
public:
 double stockPrice;
 double data;
 double volatility;
 double riskFreeRate;
 BlackScholesModel();
 BlackScholesModel( double stockPrice ); // key line
};
```

Doing this means that C++ will now automatically convert doubles into instances of BlackScholesModel. This is a very odd thing to do, and is undesirable. To prevent this unwanted behaviour, you should mark constructors that take one parameter as explicit.

```
class BlackScholesModel {
public:
 double stockPrice;
 double data;
 double volatility;
 double riskFreeRate;
 BlackScholesModel();
 explicit BlackScholesModel( double stockPrice ); // key line
};
```

The code above prevents automatic conversion. In the very rare event that automatic conversion is useful (as for strings) you can drop the explicit.

If you forget the explicit it isn't the end of the world. The confusions that may arise from forgetting to use it are quite rare in practice.

# Exercises

8.8.1 Write a default constructor for every class that you have created so far. Use both forms of the constructor syntax to familiarise yourself with the options.

8.8.2 Write a class Polynomial that represents the polynomial

> $a_{0}+a_{1}x+a_{2}x^{2}+...+x^{n}.$

Here the coefficients $a_{i}$ are doubles which associated with the polynomial itself, but $x$ is an unknown.

The class Polynomial should have the following features.