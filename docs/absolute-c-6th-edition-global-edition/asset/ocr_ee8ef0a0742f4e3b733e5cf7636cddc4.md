# Display 8.5 Overloading << and >> (part 2 of 3)

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
31
32    int dollarsPart(double amount) const;
33    int centsPart(double amount) const;
34    int round(double number) const;
35    };
36
37    int main()
38    {
39        Money yourAmount, myAmount(10, 9);
40        cout << "Enter an amount of money: ";
41        cin >> yourAmount;
42        cout << "Your amount is " << yourAmount << endl;
43        cout << "My amount is " << myAmount << endl;
44
45        if (yourAmount == myAmount)
46            cout << "We have the same amounts.\n";
47        else
48            cout << "One of us is richer.\n";
49
50        Money ourAmount = yourAmount + myAmount;
51        cout << yourAmount << " + " << myAmount
52             << " equals " << ourAmount << endl;
53
54        Money diffAmount = yourAmount - myAmount;
55        cout << yourAmount << " - " << myAmount
56             << " equals " << diffAmount << endl;
57
58        return 0;
59    }

    <Definitions of other member functions are as in Display 8.1.
    Definitions of other overloaded operators are as in Display 8.3.>
```

> Since << returns a reference, you can chain << like this. You can chain >> in a similar way.