
instead of having to use the member function output as shown here:

```
Money amount(100);
cout << "I have ";
amount.output( );
cout << " in my purse.\n";
```

One problem in overloading the operator << is deciding what value, if any, should be returned when << is used in an expression like the following:

```
cout << amount
```

The two operands in the previous expression are cout and amount, and evaluating the expression should cause the value of amount to be written to the screen. But if << is an operator like + or -, then the previous expression should also return some value. After all, expressions with other operands, such as n1 + n2, return values. But what does cout << amount return? To obtain the answer to that question, we need to look at a more complicated expression involving <<.

Let us consider the following expression, which involves evaluating a chain of expressions using <<:

```
cout << "I have " << amount << " in my purse.\n";
```

If you think of the operator << as being analogous to other operators, such as +, then the latter expression should be (and in fact is) equivalent to the following:

```
( { cout << "I have " } << amount ) << " in my purse.\n";
```

What value should << return to make sense of the previous expression? The first thing evaluated is the subexpression:

```
(cout << "I have ")
```

If things are to work out, then the previous subexpression had better return cout so that the computation can continue as follows:

```
{ cout << amount } << " in my purse.\n";
```

And if things are to continue to work out, (cout << amount) had better also return cout so that the computation can continue as follows:

```
cout << " in my purse.\n";
```

This is illustrated in Display 8.4. The operator << should return its first argument, which is of type ostream (the type of cout).

Thus, the declaration for the overloaded operator << (to use with the class Money) should be as follows:

```
class Money
{
public:
...
friend ostream& operator <<(ostream& outs,
    const Money& amount);
```

chains of <<

<< returns a stream

## Display 8.4 << as an Operator

```
cout << "I have " << amount << " in my purse.\n";
```

means the same as

```
((cout << "I have ") << amount) << " in my purse.\n";
```

and is evaluated as follows:

First evaluate (cout << "I have "), which returns cout:

```
((cout << "I have ") << amount) << " in my purse.\n";
```

The string "I have " is output.

```
(cout << amount) << " in my purse.\n";
```

Then evaluate (cout << amount), which returns cout:

```
(cout << amount) << " in my purse.\n";
```

The value of amount is output.

```
cout << " in my purse.\n";
```

Then evaluate cout << " in my purse.\n", which returns cout:

```
cout << " in my purse.\n";
```

The string "in my purse.\n" is output.

```
cout;
```

Since there are no more << operators, the process ends.

Once we have overloaded the insertion (output) operator <<, we will no longer need the member function output and will delete output from our definition of the class Money. The definition of the overloaded operator << is very similar to the member function output. In outline form, the definition for the overloaded operator is as follows:

```
ostream& operator <<(ostream& outputStream, const Money& amount)
{
    /*This part is the same as the body of
    Money::output which is given in Display 8.1 (except that
    dollars is replaced with amount.dollars
    and cents is replaced by amount.cents).*/
    return outputStream;
}
```

## References and More Overloaded Operators

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

## Display 8.5 Overloading << and >> (part 2 of 3)

```
16    friend const Money operator +(const Money& amount1,
17                                 const Money& amount2);
18    friend const Money operator -(const Money& amount1,
19                                 const Money& amount2);
20    friend bool operator ==(const Money& amount1,
21                           const Money& amount2);
22    friend const Money operator -(const Money& amount);
23    friend ostream& operator <<(ostream& outputStream,
24                               const Money& amount);
25    friend istream& operator >>(istream& inputStream, Money& amount);
26    private:
27        //A negative amount is represented as negative dollars
28        //and negative cents. Negative $4.50 is represented as
29        //-4 and -50.
30        int dollars, cents;

31    int dollarsPart(double amount) const;
32    int centsPart(double amount) const;
33    int round(double number) const;
34    };

35    int main()
36    {
37        Money yourAmount, myAmount(10, 9);
38        cout << "Enter an amount of money: ";
39        cin >> yourAmount;
40        cout << "Your amount is " << yourAmount << endl;
41        cout << "My amount is " << myAmount << endl;

42        if (yourAmount == myAmount)
43            cout << "We have the same amounts.\n";
44        else
45            cout << "One of us is richer.\n";

46        Money ourAmount = yourAmount + myAmount;
47        cout << yourAmount << " + " << myAmount
48             << " equals " << ourAmount << endl;

49        Money diffAmount = yourAmount - myAmount;
50        cout << yourAmount << " - " << myAmount
51             << " equals " << diffAmount << endl;

52        return 0;
53    }

    <Definitions of other member functions are as in Display 8.1.
    Definitions of other overloaded operators are as in Display 8.3.>
```

> Since << returns a reference, you can chain << like this. You can chain >> in a similar way.

## Self-Test Exercises

- 9. In Display 8.5, the definition of the overloaded operator << contains lines like the following:
  
  ```cpp
  outputStream << "$-";
  ```
  
  Is this not circular? Are we not defining << in terms of <<?

- 10. Why can we not overload << or >> as member operators?

- 11. Following is the definition for a class called Percent. Objects of type Percent represent percentages such as 10% or 99%. Give the definitions of the overloaded operators >> and << so that they can be used for input and output with objects of the class Percent. Assume that input always consists of an integer followed by the character '%', such as 25%. All percentages are whole numbers and are stored in the int member variable named value. You do not need to define the other overloaded operators and do not need to define the constructor. You only have to define the overloaded operators >> and <<.
  
  ```cpp
  #include <iostream>
  using namespace std;
  class Percent
  {
  public:
      friend bool operator ==(const Percent& first,
                              const Percent& second);
      friend bool operator <(const Percent& first,
                             const Percent& second);
      Percent();
      friend istream& operator >>(istream& inputStream,
                                  Percent& aPercent);
      friend ostream& operator <<(ostream& outputStream,
                                  const Percent& aPercent);
      //There would normally also be other members and friends.
  private:
      int value;
  };
  ```

## TIP: What Mode of Returned Value to Use

A function can return a value of type T in four different ways:

- By plain old value, as in the function declaration `T f();`
- By constant value, as in the function declaration `const T f();`
- By reference, as in the function declaration `T& f();`
- By `const` reference, as in the function declaration `const T& f();`
