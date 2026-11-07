```
```cpp
25.  void initialize(int& x, double& y, string& str)
     {
         x = 0;
         y = 0;
         str = "";
     }
```
```

```
```text
27.  7, 0, 0
     1, 0, 8
     8, 1, 8
     2, 1, 1
```
```

```
```cpp
29.  #include <iostream>

     using namespace std;

     int secret(int, int);

     void func(int x, int& y);

     int main()
     {
         int num1, num2;

     __1__    num1 = 6;

     __2__    cout << "Enter a positive integer: ";
     __3__    cin >> num2;
     __4__    cout << endl;
     __8__    cout << secret(num1, num2) << endl;
     __9__    num2 = num2 - num1;
     __10__   cout << num1 << " " << num2 << endl;
     __15__   func(num2, num1);
     __16__   cout << num1 << " " << num2 << endl;

     __17__   return 0;
     }

     int secret(int a, int b)
     {
         int d;

     __5__    d = a + b;
     __6__    b = a * d;

     __7__    return b;
     }

     void func (int x, int& y)
     {
         int val1, val2;
```
```