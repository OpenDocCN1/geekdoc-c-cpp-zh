# Operator Overloading 575

```
int main() {
  Rect r(10, 20);
  cout << r; // Translated to operator(cout, r).
  return 0;
}
```

Let me ask you, could the reference to out be const? No, because writing to out changes its status. Note that the argument is reference to const because we cannot copy an ostream object. Usually, the second parameter is declared as a reference to const not to avoid copying the argument but also the function does not change its status. Besides cout, we can also pass other ostream objects (or derived as we'll see in Chapter 20) to the function. For example, the cerr, which by default directs the output to the screen. And cerr can be redirected, out to be sent to a file. We also see that depending on the type of the passed ostream object, we can use the operator<< function to direct the output either to the screen or to a file.

Another question, suppose that the r1 and r2 objects are declared, could we use the following statement and function:

```
cout << r1 << r2;
```

To answer that question, we analyse the part of the statement. The statement is executed from left to right, that is, equivalent to: (cout << r1) << r2;
Therefore, the cout << r1, calls the operator<<(cout, r1); will be executed first. Fine, and what does it return? Nothing, so we continue with the << r2 part. What should be the return type? What be of the left of r1. In particular, it should be a reference to an ostream object, so that the execution of the statement continues. Thus, we change the function definition to:

```
ostream& operator<<(ostream& out, const Rect& r) {
  out << r.length << ' ' << r.height << '\n';
  return out;
}
```

Because it is by reference, each time the function is called it always returns the object passed to it, that is, cout. The statement cout << r1 << r2; runs normally. Specifically, the first part cout << r1 displays the dimensions of r1 and it is returned by the return value, that is, cout. So the original statement becomes << r2 and displays the dimensions of r2.

Actually, this is how the overloaded functions in ostream work for the various basic data types. In particular, they return a reference to ostream. For example, the prototype for displaying integers is similar to:

```
ostream& operator<<(int);
```

Thus, the << operator can be used sequentially in statements as:

```
int a = 10, b = 20;
cout << a << ' ' << b;
```

The expression cout << ' ' triggers a call to cout.operator<<(int), which displays the value of a and returns a reference to the invoking object, that is, cout. Thus, the original statement becomes cout << ' ' << b; and we continue accordingly.

And of course, we can format the output as we are used to. For example, to write:

```
cout << "First:" << r1 << "Second:" << r2;
```