# References and More Overloaded Operators

Note that the operator returns a reference.

The extraction operator >> is overloaded in a way that is analogous to what we described for the insertion operator <<. However, with the extraction (input) operator >>, the second argument will be the object that receives the input value, so the second parameter must be an ordinary call-by-reference parameter. In outline form the definition for the overloaded extraction operator >> is as follows:

```
istream& operator >> (istream& inputStream, Money& amount)
{
    /*This part is the same as the body of
      Money::input, which is given in Display 8.1 (except that
      dollars is replaced with amount.dollars
      and cents is replaced by amount.cents).*/

    return inputStream;
}
```

The complete definitions of the overloaded operators << and >> are given in Display 8.5, where we have rewritten the class Money yet again. This time we have rewritten the class so that the operators << and >> are overloaded to allow us to use these operators with values of type Money.

Note that you cannot realistically overload >> or << as member operators. If << and >> are to work as we want, then the first operand (first argument) must be cout or cin (or some file I/O stream). But if we want to overload the operators as members of, say, the class Money, then the first operand would have to be the calling object and so would have to be of type Money, and that will not allow you to define the operators so they behave in the normal way for >> and <<.

```
1  #include <iostream>
2  #include <cstdlib>
3  #include <cmath>
4  using namespace std;

5  //Class for amounts of money in U.S. currency
6  class Money
7  {
8  public:
9      Money( );
10     Money(double amount);
11     Money(int theDollars, int theCents);
12     Money(int theDollars);
13     double getAmount( ) const;
14     int getDollars( ) const;
15     int getCents( ) const;
```