```
cout << "Enter the number for" << "Object" << ++count << "\n";
cin >> num;
}
void operator +(demo_sum temp)
{
int x;
x=num +temp.num;
cout << "Sum of two is " << x << endl;
}
void show()
{
cout << "The num is" << num << endl;
}
};
int demo_sum : :count;
void main()
{
clrscr();
demo_sum d1,d2;
d1.input();
d1.show();
d2.input();
d2.show();
d1 + d2;
getch();
}
```

OUTPUT :
Enter the number forObject1
23
The num is23
Enter the number forObject2
45
The num is45
Sum of two is 68