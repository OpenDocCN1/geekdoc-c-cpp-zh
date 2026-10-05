# 740 Introduction to C++

```
cout << "Enter name: ";
getline(cin, name);
acnt.create_acnt(name,amnt);
break;
}
catch(const Err_Rpt& err)
{
    cout << err.msg;
}
try {
    cout << "Enter amount to deposit: ";
cin >>amnt;
acnt.deposit(amnt);

    cout << "Enter amount to withdraw: ";
cin >>amnt;
acnt.withdraw(amnt);
} catch(const Err_Rpt& err)
{
    cout << err.msg;
    return 0;
}
acnt.show();
```

C.23 Define the Circle class with private member the radius of the circle (e.g., Rad). From the Circle derive with public access the Ellipse class with private member the semi-major axis of the ellipse (e.g., axis). Define the f() function which takes as parameters a reference to an object and an integer value and subtracts them. Add appropriate functions in the classes so that the following program works.

```
int main() {
    Circle cir(5); // The radius of the circle should become 5.
    Ellipse ell(10, 6); /* The radius of the circle should become 10 and
the axis of the ellipse. */ The constructor of the Ellipse should call the
constructor of the Ellipse. */
    Circle r1 = cir, r2 = ell;
    /* The Following calls of f() should be placed in a try-catch section
and if an exception occurs the program should catch it, display a
corresponding message and terminate. */
    f(r1, 3);
    f(r2, 1);
    f(r2, 10);
    return 0;
}

void f(????& &c, int n) // Find the reference type.
{
    ???? tmp = c-n; /* Find the type of tmp. If the type of c is Circle,
the function should make the subtraction and reduce the radius of c by n.
```