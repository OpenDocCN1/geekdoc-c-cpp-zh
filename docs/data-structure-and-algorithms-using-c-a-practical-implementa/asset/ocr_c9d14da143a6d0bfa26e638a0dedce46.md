```
public :
fibo(int);
void generate();
},
fibo :: fibo(int x)
{
a=0;
b=1;
c=a+b;
n=x;
}
void fibo :: generate()
{
cout<<"THE FIBONACCI SERIES NUMBERS ARE";
cout<<endl<<a<<setw(4)<<cb;
for(int i=3;i<=n;i++)
{
c=a+b;
cout<<setw(4)<<c;
a=b;
b=c;
}
}
void main()
{
int n;
cout<<"Enter how many digits U want to print";
cin>>n;
fibo obj(n);
clrscr();
obj.generate();
}
```

# OUTPUT

```
Enter how many digits U want to print 8
THE FIBONACCI SERIES NUMBERS ARE
0 1 1 2 3 5 8 13
```

# 4.11.1.4 Copy Constructor

The copy constructor is a special type of constructor where the data members are initialized by the object. So when there is a need that the initialization should be by the object than use the copy constructor. The format is same as the parameter constructor except that the argument of the constructor should be always the object.