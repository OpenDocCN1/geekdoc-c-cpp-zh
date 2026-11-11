```
Complex add(Complex t)
{
    Complex res;
    res.real=real+t.real;
    res.imag=imag + t.img;
    return res;
}
void output()
{
    cout<<"Real part is "<<real<<"Img part is "<<img;
}
};
void main()
{
Complex C1,C2,C3;
cout<<"Enter first Complex number"<<endl;
C1.input();
cout<<"Enter second Complex number"<<endl;
C2.input();
C3 = C1.add(C2);
cout<<"Result Complex number is"<<endl;
C3.output();
}
```

# Output:

```
Enter first Complex number
10 5
Enter second Complex number
3 25
Result Complex number is
Real part is 13 Img part is 30
```

Let us understand the code from the first line of the main() function.

The statement

```
Complex C1,C2,C3;
```

creates three objects of class Complex. Following this we take the real and img values of two complex numbers C1 and C2 as input from the user by invoking the input() function over each of the objects as shown below:

```
C1.input();
C2.input();
```