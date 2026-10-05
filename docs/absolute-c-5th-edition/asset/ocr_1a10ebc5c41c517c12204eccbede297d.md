# Basic Operator Overloading 325

# Display 8.1 Operator Overloading (part 2 of 5)

```
40  if (yourAmount == myAmount)
41      cout << "We have the same amounts.\\n"
42  else
43      cout << "One of us is richer.\\n";
```

```
44  Money ourAmount = yourAmount + myAmount;
45      yourAmount.output( ); cout << " + " + myAmount.output( );
46      cout << " equals " + ourAmount.output( ); cout << endl;
```

```
47  Money diffAmount = yourAmount - myAmount;
48      yourAmount.output( ); cout << " - " + myAmount.output( );
49      cout << " equals " + diffAmount.output( ); cout << endl;
```

Note that we need to use accessor and mutator functions.

```
52 const Money operator+(const Money& amount1, const Money& amount2)
53 {
54     int intCents1 = amount1.getCents() + amount1.getDollars( ) *100;
55     int intCents2 = amount2.getCents() + amount2.getDollars( ) *100;
56     int sumAllCents = intCents1 + intCents2;
57     int absAllCents = abs(sumAllCents); //Money can be negative.
58     int finalDollars = absAllCents / 100;
59     int finalCents = absAllCents % 100;
```

```
60 if (sumAllCents < 0)
61 {
62     finalDollars = -finalDollars;
63     finalCents = -finalCents;
64 }
```

> If the return statements puzzle you, you see the tipinted \"A Constructor Can Return an Object.\"

```
65 return Money(finalDollars, finalCents);
66 }
```

```
67 //Uses stdlib.h
68 const Money operator-(const Money& amount1, const Money& amount2)
69 {
70     int intCents1 = amount1.getCents() + amount1.getDollars( ) *100;
71     int intCents2 = amount2.getCents() + amount2.getDollars( ) *100;
72     int diffAllCents = intCents1 - intCents2;
73     int absAllCents = abs(diffAllCents);
74     int finalDollars = absAllCents / 100;
75     int finalCents = absAllCents % 100;
```

```
76 if (diffAllCents < 0)
77 {
78     finalDollars = -finalDollars;
```

(continued)