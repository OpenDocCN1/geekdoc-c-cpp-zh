# Display 6.2 A Structure with a Structure Member (part 2 of 2)

```
45 }
46 //uses iostream:
47 void getCDData(CDAccount& theAccount)
48 {
49   cout << "Enter account initial balance: $";
50   cin >> theAccount.initialBalance;
51   cout << "Enter account interest rate: ";
52   cin >> theAccount.interestRate;
53   cout << "Enter the number of months until maturity: ";
54   cin >> theAccount.term;
55   cout << "Enter the maturity date:\n";
56   getDate(theAccount.maturity);
57 }
```

```
58 //uses iostream
59 void getDate(Date& theDate)
60 {
61   cout << "Enter month: ";
62   cin >> theDate.month;
63   cout << "Enter day: ";
64   cin >> theDate.day;
65   cout << "Enter year: ";
66   cin >> theDate.year;
67 }
```

# Sample Dialogue

```
Enter account data on the day account was opened:
Enter account initial balance: $100.00
Enter account interest rate: 10.0
Enter the number of months until maturity: 6
Enter the maturity date:
Enter month: 2
Enter day: 14
Enter year: 1899
When the CD matured on 2-14-1899
it had a balance of $105.00
```

# Initializing Structures

You can initialize a structure at the time that it is declared. To give a structure variable a value, follow it by an equal sign and a list of the member values enclosed in braces. For example, the following definition of a structure type for a date was given in the previous subsection:

```
struct Date
{
  int month;
```