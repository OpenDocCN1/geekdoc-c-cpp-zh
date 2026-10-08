Similarly, **Axis::move()** moves all the parts of the e **Axis** together:

```
```cpp
void Axis::move(int dx, int dy)
{
    Shape::move(dx,dy);
    notches.move(dx,dy);
    label.move(dx,dy);
}
```
```

# ### 15.5 Approximation

Here we give another small example of graphing a function: we “animate” the calculation of an exponential function. The purpose is to help you get a feel for mathematical functions (if you haven’t already), to show the way graphics can be used to illustrate computations, to give you some code to read, and finally to warn about a common problem with computations.

One way of computing an exponential function is to compute the series

$$ e^{x} == 1 + x + x^{2}/2! + x^{3}/3! + x^{4}/4! + \ldots $$

The more terms of this sequence we calculate, the more precise our value of $e^{x}$ becomes; that is, the more terms we calculate, the more digits of the result will be mathematically correct. What we will do is to compute this sequence and graph the result after each term. The exclamation point here is used with the common mathematical meaning; factorial; that is, we graph these functions in order:

```
```cpp
exp0(x)= 0           // no terms
exp1(x)= 1           // one term
exp2(x)= 1+x         // two terms; pow(x,1)/fac(1)==x
exp3(x)= 1+x+pow(x,2)/fac(2)
exp4(x)= 1+x+pow(x,2)/fac(2)+pow(x,3)/fac(3)
exp5(x)= 1+x+pow(x,2)/fac(2)+pow(x,3)/fac(3)+pow(x,4)/fac(4)
... 
```
```

Each function is a slightly better approximation of $e^{x}$ than the one before it. Here, **pow(x,n)** is the standard library function that returns $x^{n}$. There is no factorial function in the standard library, so we must define our own:

```
```cpp
int fac(int n)          // factorial(n); n!
{
    int r=1;
    while (n>1) {
        r*=n;
        --n;
    }
```
```