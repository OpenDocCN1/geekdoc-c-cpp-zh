# DISPLAY 11.8 Overloading << and >> (part 4 of 4)

```
100  int digitToInt(char c)
101  {
102      return ( static_cast<int>(c) - static_cast<int>('0') );
103  }
104  //Uses cstdlib and iostream:
105  ostream& operator<<(ostream& outs, const Money& amount)
106  {
107      long positiveCents, dollars, cents;
108      positiveCents = labs(amount.allCents);
109      dollars = positiveCents/100;
110      cents = positiveCents%100;
111
112      if (amount.allCents < 0)
113          outs << "- $" << dollars << '.';
114      else
115          outs << "$" << dollars << '.';
116
117      if (cents < 10)
118          outs << '0';
119      outs << cents;
120
121      return outs;
122  }
```

<The definitions of the member functions and other overloaded operators go here. See Displays 11.3, 11.4, 11.5, and 11.6 for the definitions.>

# infile.dat
(Not changed by program.)

# outfile.dat
(After program is run.)

```
$1.11 $2.22
$3.33
```

```
$1.11 copied from the file infile.dat.
```

# Screen Output

```
$1.11 copied from the file infile.dat.
```