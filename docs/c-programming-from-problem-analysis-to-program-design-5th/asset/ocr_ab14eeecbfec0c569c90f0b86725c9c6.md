```
```cpp
int main()
{
    string firstName, lastName;
    int num;
    double salary;

    cout << "Enter first name: ";
    cin >> firstName;
    cout << endl;

    cout << "Enter last name: ";
    cin >> lastName;
    cout << endl;

    cout << "Enter a positive integer less than 70: ";
    cin >> num;
    cout << endl;

    salary = num * X;

    cout << "Name: " << firstName << BLANK << lastName << endl;
    cout << "Wages: $" << salary << endl;
    cout << "X = " << X << endl;
    cout << "X + Y = " << X + Y << endl;

    return 0;
}
```
```

# Chapter 3

+   1. a. true; b. true; c. false; d. false; e. true; f. true
+   3. a. x = 37, y = 86, z = 0.56
+      b. x = 37, y = 32, z = 86.56
+      c. Input failure: z = 37.0, x = 86, trying to read the . (period) into y.
+   5. Input failure: Trying to read A into y, which is an int variable. x = 46, y = 18, and z = 'A'. The values of y and z are unchanged.
+   7. iomanip
+   9. getline(cin, name);
+   11. a. name = "Lance Grant", age = 23
+       b. name = "", age = 23
+   13. 
+       ```cpp
+       #include <iostream>
+       #include <fstream>
+   
+       using namespace std;
+   
+       int main()
+       {
+           int num1, num2;
+           ifstream infile;
+           ostream outfile;
+       ```