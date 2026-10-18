```
```cpp
int main()
{
    cout << "Integer coefficients \n";
    roots(1,-5,6);
    cout << "\nFloat coefficients \n";
    roots(1.5,3.6,5.0);

    return 0;
}
```
```

The output of Program 12.7 would be:

Integer coefficients
Roots are real

R1 = 3 and R2 = 2

Float coefficients
Roots are complex
Real part = -1.2
Imaginary part = 1.375985

# 12 Function Templates with Multiple Parameters

Like template classes, we can use more than one generic data type in the template statement, using a comma-separated list as shown below:

```
```cpp
template<class T1, class T2, ...>
returntype functionname (arguments of types T1, T2,...)
{
    ....
}
```
```