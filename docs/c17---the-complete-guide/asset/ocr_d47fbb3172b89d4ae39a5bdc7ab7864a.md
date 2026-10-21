# # Chapter 9

# ## Class Template Argument Deduction

Before C++17, you always had to explicitly specify all template arguments for class templates. For example, you cannot omit the double here:

std::complex<double> c{5.1,3.3};
or omit the need to specify std::mutex here a second time:

std::mutex mx;
std::lock_guard<std::mutex> lg(mx);

Since C++17, the constraint of always having to specify the template arguments explicitly has been relaxed. By using class template argument deduction (CTAD), you can omit explicit definition of the template arguments if the constructor is able to deduce all template parameters.

For example:

+   - You can now declare:
+   
+   std::complex c{5.1,3.3}; // OK: std::complex<double> deduced

+   - You can now implement:
+   
+   std::mutex mx;
+   std::lock_guard lg{mx}; // OK: std::lock_guard<std::mutex> deduced

+   - You can even let containers deduce element types:
+   
+   std::vector v1 { 1, 2, 3 } // OK: std::vector<int> deduced
+   
+   std::vector v2 {"hello", "world"}; // OK: std::vector<const char*> deduced



Class template argument deduction can be used whenever the arguments passed to a constructor can be used to deduce the class template parameters. The deduction supports all methods of initialization (provided the initialization itself is valid):

```
std::complex c1{1.1, 2.2}; // deduces std::complex<double>
std::complex c2{2.2, 3.3}; // deduces std::complex<double>
```