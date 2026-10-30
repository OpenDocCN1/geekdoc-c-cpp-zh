```
h() = 7;
}
```

The function call h() will return a reference to the local variable x of the function. Unfortunately, after the function returns, the local variable will no longer exist! Thus in the main program it will be incorrect to either modify h() or get its value. Note that most C++ compilers will not give any errors for the code above. However, this code is definitely incorrect.

Similar ideas apply to returning pointers. The analogue of the first example above is as follows.

```
int *f(int *x, int *y){
    if(*x > *y) return x;
    else return y;
}
int main(){
    int p=5, q=4;
    *f(&p,&q) = 2;
    cout << p << ',' << q << endl;
    cout << *f(&p,&q) << endl;
}
```

In this, the call f(&p,&q) returns the address of a variable, so it can be dereferenced and then we can either modify the variable or get its value. Thus the first print statement will print "2 4" and the second will print 4 as before.

Analogously it is incorrect to return the address of a variable that will be deallocated by the time the address can be used.

```
double *h(){
    double x = 5;
    return &x;
}
int main(){
    *h() = 7;
}
```

The function call h() returns the address of the variable x local to the function call. The variable is destroyed when the function call returns. Hence it is incorrect to use h() in any way in main.

# 9.10 Default values of parameters

It is possible to assign default values to parameters of a function. If a particular parameter has a default value, then the corresponding argument may be omitted while calling it. The default value is specified by writing it as an assignment to the parameter in the parameter list of the function definition. Here is a polygon function in which both parameters have default values.