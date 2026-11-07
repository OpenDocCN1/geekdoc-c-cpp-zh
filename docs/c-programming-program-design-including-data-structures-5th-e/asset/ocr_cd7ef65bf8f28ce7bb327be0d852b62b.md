+   17. ```cpp
+    double funcEx17(double x, double y, double z)
+   {
+       return (x + y) * z;
+   }
+   ```

# Chapter 7

+   1. a. true; b. false; c. true; d. false; e. true; f. false; g. false; h. false; i. true

+   3.
+      a. A variable declared in the heading of a function definition is called a formal parameter. A variable or expression used in a function call is called an actual parameter.
+      b. A value parameter receives a copy of the actual parameter’s data. A reference parameter receives the address of the actual parameter.
+      c. A variable declared within a function or block is called a local variable. A variable declared outside of every function definition is called a global variable.

+   5. ```cpp
+   void funcThreeTimes(double x)
+   {
+       cout << fixed << showpoint << setprecision(2);
+       cout << 3 * x << endl;
+   }
+   ```

+   7. ```cpp
+   void initialize(int& x, double& y, string& str)
+   {
+       x = 0;
+       y = 0;
+       str = "";
+   }
+   ```

+   9.
+      5, 10, 15
+      20, 10, 15
+      25, 30, 15
+      45, 30, 15

+   11. ```cpp
+   #include <iostream>
+   
+   using namespace std;
+   
+   void func(int val1, int val2);
+   
+   int main()
+   {
+       int num1, num2;
+       __1__ cout << "Please enter two integers." << endl;
+       __2__ cin >> num1 >> num2;
+       __3__ func(num1, num2);
+   }
+   ```