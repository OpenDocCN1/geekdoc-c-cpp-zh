# Display 7.2  `BankAccount` Class (part 5 of 6)

```
```cpp
134
135 void BankAccount::setBalance(double balance)
136 {
137     accountDollars = dollarsPart(balance);
138     accountCents = centsPart(balance);
139 }
140
141 //Uses cstdlib:
142 void BankAccount::setBalance(int dollars, int cents)
143 {
144     if ((dollars < 0 && cents > 0) || (dollars > 0 && cents < 0))
145     {
146         cout << "Inconsistent account data.\n";
147         exit(1);
148     }
149     accountDollars = dollars;
150     accountCents = cents;
151 }
152
153 //Uses cstdlib:
154 void BankAccount::setRate(double newRate)
155 {
156     if (newRate >= 0.0)
157         rate = newRate;
158     else
159     {
160         cout << "Cannot have a negative interest rate.\n";
161         exit(1);
162     }
163 }
164 int BankAccount::dollarsPart(double amount)
165 {
166     return static_cast<int>(amount);
167 }
168 //Uses cmath:
169 int BankAccount::centsPart(double amount)
170 {
171     double doubleCents = amount * 100;
172     int intCents = (round(fabs(doubleCents))) % 100;
173     //% can misbehave on negatives
174     if (amount < 0)
175         intCents = -intCents;
176     return intCents;
177 }
178
179 //Uses cmath:
180 int BankAccount::round(double number)
181 {
182     return static_cast<int>(floor(number + 0.5));
183 }
```
```

> *This could be a regular function rather than a member function, but as a member function we are able to make it private.*

> *These could be regular functions rather than member functions, but as member functions we were able to make them private.*

> *If this does not seem clear, see the discussion of round in Chapter 3, Section 3.2.*