```
```cpp
double x1=1.0, y1=1.0, r1, theta1;
Cartesian_To_Polar(x1,y1,r1,theta1);
cout << r1 << ", " << theta1 << endl;
}
```
```

Here is how the call `CartesianToPolar(x1,y1,r1,theta1)` executes. The values of x1,y1 are copied to the corresponding parameters x1,y1. However, as mentioned, the values of r1, theta1 are not copied. Instead, all references to r, theta in the function are deemed to be references to the variables r1,theta1 instead! Thus, as CartesianToPolar executes, the assignments in the statement `r=...` and `theta=...` get made to r1 and theta1 directly. So indeed, when the function returns, the variable r1 would contain √(1+1) = √2 ≈ 1.4142, and theta1 would contain tan⁻¹1 = π/4 ≈ 0.785, and these would be printed out.

The function to swap two variables can also be written in a similar manner.

```
```cpp
void swap2(int &a, int &b){
    int temp;
    temp = a;
    a = b;
    b = temp;
}
```
```

This can be called as follows.

```
```cpp
int main{
    int x=5, y=6;
    swap2(x,y);
    cout << x << " " << y << endl;
}
```
```

Both the arguments of `swap2` are references, and so nothing is copied into the activation area of swap2. The parameters a,b refer directly to x,y, i.e. effectively we execute

```
```cpp
temp = x;
x = y;
b = temp;
```
```

This will clearly exchange the values of x,y, so at the end “6 5” will be printed.

Our last example is the `read_marks_into` function discussed in Section 9.6.

```
```cpp
bool read_marks_into(int &var){
    cin >> var;
    return var != 200;
}
```
```

This definition will work as desired with the main program given in Section 9.6. When the function executes, the first line will read a value into var. But var is a reference for the corresponding parameter nextmark, and hence the value will in fact be read into nextmark. The expression var != 200 is true if var is not 200, and false if it is 200. So the while loop in the main program will indeed terminate as soon as 200 is read. Continuing the discussion at the end of Section 7.2, we note that perhaps this is the nicest way of writing the mark averaging program: we do not duplicate any code, and yet the loop termination is by checking a condition at the top, rather than using a break statement in the body.