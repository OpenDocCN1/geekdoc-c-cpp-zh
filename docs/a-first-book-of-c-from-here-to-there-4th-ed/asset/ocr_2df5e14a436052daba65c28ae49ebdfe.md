# Table 3.4 ostream Class Methods

| Method | Comment | Example |
|---|---|---|
| precision(n) | Equivalent to setprecision() | cout.precision(2) |
| fill('x') | Equivalent to setfill() | cout.fill('*') |
| setf(ios::fixed) | Equivalent to cout.setf(ios::fixed) | setiosflags(ios::fixed) |
| setf(ios::showpoint) | Equivalent to cout.setf(ios::showpoint) | setiosflags(ios::showpoint) |
| setf(ios::left) | Equivalent to left | cout.setf(ios::left) |
| setf(ios::right) | Equivalent to right | cout.setf(ios::right) |
| setf(ios::flush) | Equivalent to endl | cout.setf(ios::flush) |

In the Example column of Table 3.4, notice that the name of the object, cout, is separated from the method with a period. As mentioned, this format is the standard way of calling a class method and providing an object for it to operate on.

![](bbox=[0.07, 0.6, 0.1, 0.68])

# EXERCISES 3.2

+   1. (Debug) Determine the errors in the following statements:
+      a. cout << "\n << " 15)
+      b. cout << "setw(4)" << 33;
+      c. cout << "setprecision(5)" << 526.768;
+      d. "Hello World!" >> cout;
+      e. cout << 47 << setw(6);
+      f. cout << set(10) << 526.768 << setprecision(2);
+   2. (Desk check) Determine and write out the display produced by the following statements:
+      a. cout << "|" << 5 << "|";
+      b. cout << "|" << setw(4) << 5 << "|";
+      c. cout << "|" << setw(4) << 56829 << "|";
+      d. cout << "|" << setw(5) << setiosflags(ios::fixed) << setprecision(2) << 5.26 << "|";
+      e. cout << "|" << setw(5) << setiosflags(ios::fixed) << setprecision(2) << 5.267 << "|";
+      f. cout << "|" << setw(5) << setiosflags(ios::fixed) << setprecision(2) << 53.264 << "|";
+      g. cout << "|" << setw(5) << setiosflags(ios::fixed) << setprecision(2) << 534.264 << "|";
+      h. cout << "|" << setw(5) << setiosflags(ios::fixed) << setprecision(2) << 534. << "|";