```
```cpp
    nu = num*obj.num;
    de = den*obj.den;
    return rat(nu,de);
}

void rat::display()                 //function to

display the rational number
{
    cout<<endl<<"The given rational number is"<<endl;
    cout<<num<<"/"<<den<<endl;
}

void main()
{
    rat r1,r2(4,10),r3;
    clrscr();
    cout<<"value of r1:";
    r1.display();
    cout<<"value of r2:";
    r2.display();
    r3=r1+r2;
    cout<<"The result of addition of rational

number";
    r3.display();

    r3=r1-r2;
    cout<<"The result of subtraction of rational

number";
    r3.display();

    r3=r1/r2;
    cout<<"The result of division of rational

number";
    r3.display();

    r3=r1*r2;
    cout<<"The result of multiplication of rational

number";
    r3.display();
}
```
```