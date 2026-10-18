```
```cpp
complex temp; //temporary
temp.x = x + c.x; // these are
temp.y = y + c.y; //float additions
return(temp);
}
void complex :: display(void)
{
    cout << x << "+j" << y << "\n";
}
int main()
{
    complex C1, C2, C3; //invokes constructor 1
    C1 = complex(2.5, 3.5); // invokes constructor 2
    C2 = complex(1.6, 2.7);
    C3 = C1 + C2;
    cout << "C1 ="; C1.display();
    cout << "C2 ="; C2.display();
    cout << "C3 ="; C3.display();
    return 0;
}
```
```

The output of Program 7.2 would be:

+   C1 = 2.5 + j3.5
+   
+   C2 = 1.6 + j2.7
+   
+   C3 = 4.1 + j6.2

> **NOTE:** *Let us have a close look at the function operator+() and see how the operator overloading is implemented.*

```
```cpp
complex complex :: operator+(complex c)
{
    complex temp;
    temp.x = x + c.x;
```
```