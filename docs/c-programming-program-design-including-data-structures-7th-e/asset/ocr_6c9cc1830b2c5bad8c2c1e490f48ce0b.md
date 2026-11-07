26. State whether the following `switch` statements. If not, explain why. Assume that n and digit are `int` variables. (11)

```
a. switch (n <= 2)
   {
   case 0:
       cout << "Draw." << endl;
       break;
   case 1:
       cout << "Win." << endl;
       break;
   case 2:
       cout << "Lose." << endl;
       break;
   }
```

```
b. switch (digit / 4)
   {
   case 0:
   case 1:
       cout << "low." << endl;
       break;
   case 1,
   case 2:
       cout << "middle." << endl;
       break;
   case 3:
       cout << "high." << endl;
   }
```

```
c. switch (n % 6)
   {
   case 1:
   case 2:
   case 3:
   case 4:
   case 5:
       cout << n;
       break;
   case 0:
       cout << endl;
       break;
   }
```

```
d. switch (n % 10)
   {
   case 2:
   case 4:
   case 6:
   case 8:
       cout << "Even";
       break;
   case 1:
   case 3:
```