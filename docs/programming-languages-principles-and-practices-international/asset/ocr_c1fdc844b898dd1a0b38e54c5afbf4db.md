by using an ampersand (&) after the data type in C++, and a var keyword before the variable name in Pascal:

```
void inc(int& x) // C++
{ x++ ; }

procedure inc(var x: integer); (* Pascal *)
begin
    x :=  x + 1;
end;
```

After a call to inc(a) the value of a has increased by 1, so that a side effect has occurred. Multiple aliasing is also possible, such as in the following example:

```
int a;

void yuck (int& x, int& y)
{ x = 2;
    y = 3;
    a = 4;
}
---
yuck (a, a);
```

Inside procedure yuck after the call, the identifiers x, y, and a all refer to the same variable, namely, the variable a.

As noted previously, C can achieve pass by reference by passing a reference or location explicitly as a pointer. C uses the operator & to indicate the location of a variable and the operator * to dereference a pointer. For example:

```
void inc (int* x) /*C imitation of pass by reference */
{ (*x)++; /* adds 1 to *x */ }
---
int a;
---
inc(&a); /* pass the address of a to the inc function */
```

This code has the same effect as the previous C++ or Pascal code for the inc procedure. Of course, there is the annoying necessity here of explicitly taking the address of the variable a, and then explicitly deferencing it again in the body of inc.

A similar effect can be achieved in ML by using reference types to imitate pass by reference. (In ML, as in C, only pass by value is available.) For example:

```
fun inc (x: int ref) = x := !x + 1;
```