```
{
    c= a+b;
    a=b;
    b=c;
    cout<<" "<<c;
}
cout << endl;
}
};

void main()
{
    Fibbo obj;
    int x;
    clrscr();
    cout<<"Enter the number of terms \n";
    cin>>x;
    obj.input(x);
    obj.gen_ser();
    getch();
}
```

# OUTPUT :

(FIRST RUN)

Enter the number of terms
7
fibbonaci series is
0 1 1 2 3 5 8

(SECOND RUN)

Enter the number of terms
8
fibbonaci series is
0 1 1 2 3 5 8 13

# EXPLANATION :

Fibonacci series is a series in which each new term is the sum of previous two terms. Initially we assume two terms are 0 and 1 so next term will be 0 + 1 = 1, next term will be 1 + 1 = 2 and so on. So, Fibonacci series is 0, 1, 1, 2, 3, 5, 8, 13, 21, 34,.......