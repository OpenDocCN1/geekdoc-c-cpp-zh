# Vectors

```
#include <vector>
vector<int> values = { 0, 1, 4, 9, 16 };
vector<string> names;
names.push_back("Ann");
names.push_back("Cindy"); // names.size() is now 2
names.pop_back(); // Removes last element
names[0] = "Beth"; // Use [] for element access
```

# Range-based for Loop

```
for (int v : values)
{
  cout << v << endl;
}
```

# Output Manipulators

+   #include <iomanip>
+   - endl  Output new line
+   - fixed  Fixed format for floating-point
+   - setprecision(n)  Number of digits after decimal point for fixed format
+   - setw(n)  Field width for the next item
+   - left  Left alignment (use for strings)
+   - right  Right alignment (default)
+   - setfill(ch)  Fill character (default: space)

# Pointers

```
int n = 10;
int* p = &n; // p set to address of n
*p = 11; // n is now 11
```

![](bbox=[0.22, 0.52, 0.48, 0.62])

```
int a[5] = { 0, 1, 4, 9, 16 };
p = a; // p points to start of a
*p = 11; // a[0] is now 11
p++; // p points to a[1]
p[2] = 11; // a[3] is now 11
```

![](bbox=[0.22, 0.75, 0.48, 0.88])

# Class Definition

```
class BankAccount
{
public:
  BankAccount(double amount); // Constructor declaration
  void deposit(double amount); // Member function declaration
  double get_balance() const; // Accessor member function
  ...
private:
  double balance; // Data member
};
void BankAccount::deposit(double amount)
{
  balance = balance + amount;
}
```

# Input and Output

```
#include <iostream>
cin >> x; // x can be int, double, string
cout << x;
while (cin >> x) { Process x }
if (cin.fail()) // Previous input failed

#include <fstream>
string filename = ...;
ifstream in(filename);
ofstream out("output.txt");
string line; getline(in, line);
char ch; in.get(ch);
```

# Inheritance

```
class CheckingAccount : public BankAccount
{
public:
  void deposit(double amount); // Member function overrides base class
private:
  int transactions; // Added data member in derived class
};
void CheckingAccount::deposit(double amount)
{
  BankAccount::deposit(amount); // Calls base class member function
  transactions++;
}
```